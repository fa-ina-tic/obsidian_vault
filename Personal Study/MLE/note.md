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

한번 모델을 콜하는 기준이 연산 반복의 기준이다.
그러면서 리퀘스트가 끝났는지에 대한 거를 감독해가지고 끝나면 바로 전달할 수 있도록 한다.
근데 위 방식은 배치 단위로 한번에 때려넣는 데에 문제가 조금 있음

각 리퀘스트가 다른수의 토큰을 생성할거 아님? 그러면 트포 친구가 해당 리퀘스트들을 배치방식으로 진행을 못함. -> 진스짱이 배치로 못하는 텐서 연산을 하는데, 이게 처리된 토큰수에 따라 늘줄 때리기 때문 -> 
-> 이게 왜 그런지는 몰?루 -> 오케이 깨달았스

자 배치 떄릴때도 생각해보자 -> 모델의 input length는 통일해서 줘야 병렬처리 이꾸 할거 아냐 -> 이때는 패딩을 때려서 -> 모델이 넣을게 = 이 느낌으로 Batch를 리퀘스트 단위로 짰을 때는 이렇게 하면 됨.

근데 이터레이션 단위이면? -> 시퀀스에 패딩 낭낭하게 채워줘서 해결되냐? -> 농 -> 진스짱은 배치 그런거 몰라~ 난 한땀한땀 때려댈거임~ 이러고 있음 -> 흠... 이해가 아직 안되네.. 백그라운드 먼저 때려보자 지금 inference가 어떤 process로 되고 있는지 보면 더 이해 잘될 것 같음.

# Background
*inference procedure of GPT*
hmm







