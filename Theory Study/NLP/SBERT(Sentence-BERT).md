BERT, RoBERT는 semantic textual similarity(STS) 같은 sentence-pair regression task에서 높은 성능을 보여옴

하지만 둘 다 문장들이 다 네트워크에 들어가야 해서, 연산을 많이 잡아먹는다.
BERT에서는 10000개의 문장들 중에서 가장 비슷한 페어를 찾는데 최대 65시간 정도 시간이 필요하다. 

이를 해결하기 위해 나온게 SBERT이다. SBERT는 siamese, triplet network를 활용해 sentence emdedding을 진행한다. 이 방식을 통해 BERT, RoBERT의 성능을 유지하면서도, 페어를 찾는데 필요한 연산량을 획기적으로 줄여준다.

BERT는 cross-encoder를 사용 : 두 문장이 encoder로 들어가고 target value가 예측된다.
이거는 사실 너무 많은 Combination을 생성함. 
10000개의 문장 사이에 가장 유사한 문장 쌍을 탐색하는 데에는 (10000 * 9999)/2번의 연산이 돌게 된다.

SBERT는 BERT/RoBERT의 output에 pooling operation을 추가한다.
-> operation in default = mean 이고, max를 사용할 수도 있음


다른 말로, 문장 속 단어들에 대한 벡터 행렬들을 한 문장으로 볼 수도 있지만, 이 벡터 속 스칼라 값들을 평균내거나 최대값으로 문장을 표현하도록 할 수도 있도록 하고, cosine similarity를 계산해서 레이블을 생성한다. -> 이걸로 semantic textual similarity 문제를 푸는 거임.

특정 문장과 유사한 정보를 가지고 있는 문장을 탐색(시멘틱 검색)을 할 때 빠르다.




