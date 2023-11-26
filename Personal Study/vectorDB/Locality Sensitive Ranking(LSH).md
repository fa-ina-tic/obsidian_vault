**아래 문서는 모두 vector data 기반 설명입니다.**

Data point를 바구니로 hash하기 위한 함수의 가족계로 사용
가까운 포인트들은 같은 바구니에 높은 확률로 남겨지고, 멀리 떨어진 포인트들은 다른 바구니에 놓이게 됨
다양한 유사성에서 관찰값들 확인
Find documents with Jaccard similarity of at least t
## Steps
![[Pasted image 20231123161557.png]]
1. Shingling
2. Min hashing
3. Locality-sensitive hashing

## Shingling
documents의 구성 요소를 k 길이의 numpy로 뱉어냄
문서들은 아래 특징을 가지고 있음
1. 비슷한 문서일수록 많은 shingles를 공유
2. 단락의 순서는 shingles에 영향을 크게 주지 않음
3. 너무 작은 K는 대부분의 문서에서 반복적으로 등장하므로 사용하지 않음

문서들 사이의 유사성 측정치
- Jaccard Index
$$J(A,B) = \frac{|A \cap B|}{|A \cup B|}$$

## [[Hashing]]
문서를 Hash 함수를 사용하여 작은 signature로 변환

d : 문서
H : 해쉬 함수
H(d)

P(H(d1) == H(d2))
hashing method
- Min-Hashing
	- 데이터의 차원을 줄여서 줄어든 차원의 정보만으로 클러스터링 하였을 때 본래 데이터의 클러스터링 결과와 거의 비슷하도록 하는 hashing method
	- J(A,B)를 빠르게 추정하기 위해 사용됨
	- 
## Locality-Sensitive Hashing(LSH)
2개의 문서의 signature를 만들었을 때, 그것이 이 두 문서들이 쌍이 
