### [[Seq2Seq]]의 단점
1. hidden state에 정보를 저장하는데, capacity가 유한하여 전체 timestep의 정보를 담기 어렵다
	1. capacity가 유한한 이유 : Input / output 문장 길이가 고정되어 있음.
	2. 문장이 길어질수록 앞에 vanishing gradient 문제가 생겨서 문맥파악을 참 못함.

위의 단점을 해결하기 위해 고안된 방법이 **Attention**

### 기본 컨셉
Decoder에서 출력 단어를 예측하는 매 시점(time step)마다, 인코더에서의 전체 입력 문장을 다시 한 번 참고한다. 이를 참고할 때, 예측해야 할 단어와 연관이 있는 입력 단어 부분을 좀 더 집중(attention)해서 참고한다.

Attention은 미분 가능한 key-value function(Differentiable Key-Value Function). 다만 Query와 Key가 완벽히 일치해야 Value를 반환하는 것이 아니라 Query와 Key의 유사도에 따라 Value 반환한다.

[[Seq2Seq]] 모델에서 (Q, K, V)는 아래와 같다:
- Q : 현재 timestep의 decoder input
- K : 각 timestep 별 encoder output
- V : 각 timestep 별 encoder output

