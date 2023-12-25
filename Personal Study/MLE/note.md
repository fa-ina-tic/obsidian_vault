ORCA

### Abstraction
Large-scale Transformer-based models trained for generation tasks
- generate next token in an autoregressive manner
	- need to run model multiple times to process an inference request
		- each iteration of the model generates a single output token for the request
so the problem is --> we should wait for prior batch of requests to be finished to give a new request to our model --> fkin freaky isnt it

so we solve this prob using iteration-level scheduling which schedules by granularity of iteration instead of request. it runs engine only a single iteration of model on the batch

plus, to use batching and iteration-level scheduling, we use selective batching. it applies batching only to a selected set of operations

based on this *iteration-level scheduling* and *selective batching*, ORCA the distributed serving system is made. it also designed for scalability to models with hundreds of billions of parameters. it is super fast:)


# Intro

Transformer models learn elements of sequence's connections to each other. -> it outperforms recurrent model

to use generative models -> often delegate the [[inference]] procedure to a separate service which is responsible for ML inference serving. the needs of low latency and high throughput increase have facilitated the development of inference serving system(ex - Triton Inference Server, Tensorflow Serving). These examples can use separately-developed DNN execution engine to perform the actual tensor operations

triton example -> it groups multiple requests into a batch. and give it to Transformer model and model conducts the inference procedure in the batched manner. -> it allows Transformer to inference requests simultaneously and increase inferencing throughput

but current inference serving system have limitations for Transformer-based generative models because we should run model several times for generating each token. if we run the inference engine for several request, engine returns inference results for the entire batch(which is requests) at once after processing all requests. It means request that ended earlier should wait for other requests to be finished and delay would be occurred. and if we separate each requests to other batch, it increase the requests' queueing time which also cause a delay.

so paper suggests to schedule the execution at the granularity of iteration, not request.
<details>  
<summary>rephrasing</summary>  
한번 모델을 콜하는 기준이 연산 반복의 기준이다.
그러면서 리퀘스트가 끝났는지에 대한 거를 감독해가지고 끝나면 바로 전달할 수 있도록 한다.
근데 위 방식은 배치 단위로 한번에 때려넣는 데에 문제가 조금 있음

각 리퀘스트가 다른수의 토큰을 생성할거 아님? 그러면 트포 친구가 해당 리퀘스트들을 배치방식으로 진행을 못함. -> 진스짱이 배치로 못하는 텐서 연산을 하는데, 이게 처리된 토큰수에 따라 늘줄 때리기 때문 -> 
-> 이게 왜 그런지는 몰?루 -> 오케이 깨달았스

자 배치 떄릴때도 생각해보자 -> 모델의 input length는 통일해서 줘야 병렬처리 이꾸 할거 아냐 -> 이때는 패딩을 때려서 -> 모델이 넣을게 = 이 느낌으로 Batch를 리퀘스트 단위로 짰을 때는 이렇게 하면 됨.

근데 이터레이션 단위이면? -> 시퀀스에 패딩 낭낭하게 채워줘서 해결되냐? -> 농 -> 진스짱은 배치 그런거 몰라~ 난 한땀한땀 때려댈거임~ 이러고 있음 -> 흠... 이해가 아직 안되네.. 백그라운드 먼저 때려보자 지금 inference가 어떤 process로 되고 있는지 보면 더 이해 잘될 것 같음.  
</details>



# Background
*inference procedure of GPT*
GPT : autoregressive language model based on Transformer
input : text
output : new text

receives a sequence of input token -> completes the sequence by generating subsequent output tokens -> see image below
![[Pasted image 20231223122612.png]]

GPT's three layer : inference procedure, Transformer layer, and internal state usage
nodes and edges indicate Transformer layers and dependencies between the layers repectively
-> node랑 edge는 트포 레이어와 레이어 간의 종속성을 나타낸다.

Transformer layers are executed in the order denoted by the numbers on the nodes. > the nodes that use the same set of model parameters are filled with the same color
-> 트포 레이어는 노드 숫자에 따라 순차적으로 진행됨. 그리고 같은 색상은 같은 매개변수를 공유함

the output token would be input token for next iteration, and it impose a sequential, one-by-one inference procedure
-> output token은 다음 iteration의 input token이 되고. 이는 직렬적인 추론 과정을 일으킨다.

This autoregressive procedure of generating single token means it should pass all the layers of model to generate single token.
-> client Input이든 이전 iteration의 output token이든 다음 한 토큰을 만들기 위해서는 모델의 모든 계층을 통과해야 한다.

in this paper, the run of all layers would be define as an iteration of the model. 
first iter1 in figure would be _initiation phase_, which is responsible for precessing the input tokens and generating the first output token
-> 모델의 모든 레이어를 통과하는 게 single iteration이다. 그림의 iter1은 첫번째 output token을 생성하는 Iteration으로, initation phase라고 정의한다.

iter2 and iter3 would be increment phase, take formal output token as input token and generates the next token. while the increment phase comprises multiple iterations, initiation phase is typically implemented as a single iteration by processing all the input tokens in parallel
-> input token 받아서 다음 output 만드는 건 increment phase. initiation phase에서는 사용자가 입력한 모든 토근을 병렬적으로 받고, increment phase에는 생성된 단 하나의 token만 input으로 받음

original Transformer employs two stacks of Transformer layers, while GPT's architecture consists of a single layer stack, namely decoder
-> 기본 트포는 두 스택의 레이어가 있는데, gpt는 decoder라고 해서 한 스택이 있음.

Attention is all you need~
Attention -> shortly, it computes a weighted average of the tokens of interest so that each token in the sequence is aware of the other
sequence 안의 토큰 끼리의 연관성을 추론함 -> sequence 길이가 N 인 경우 $N^2$의 attention array 생성됨

attention input: query, key, value
process
1. computes dot products of the query with all keys
2. applies Softmax on the dot products to get weights
3. conducts weighted average of all values associated with the weights

keys and values should conisidered as internal states because attention requires keys and values of all preceding tokens.

naive procedure would be taking all tokens in the sequence and recompute all the keys and values at every iteration.

