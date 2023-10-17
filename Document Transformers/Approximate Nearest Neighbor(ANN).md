Nearest Neighbor 연산은 벡터 수가 늘수록 연산 시간을 기하급수적으로 많이 소요하는, 비싼 연산이 된다. 

이러한 이유로 nearest neighbor 연산은 bottleneck 으로 자주 지목되는데, 이를 해결하기 위해 100% 정확도가 아닌 임의의 높은 정확도로 근접한 Vector를 빠르게 찾는 ANN[관련 자료](https://github.com/spotify/annoy)  가 발표되었다.

연산 방법
1. Vector 공간을 권역으로 잘게 나눈다.
2. 잘게 나누어진 공간을 binary tree로 구성한다.
3. Nearest Neighbor 연산을 하고자 하면, 해당 vector가 포함되는 공간을 tree 검색으로 찾고 찾은 권역 내에서 Nearest Neighbor 연산을 진행한다.