Spotify에서 개발한 tree-based ANN 기법
주어진 vector들을 여러개의 subset으로 나누어 tree형태의 자료구조로 구성하고 이를 활용하여 탐색하는 기법
![[Pasted image 20231124111538.png]]
 $$시간 복잡도 : O(LogN)$$

특징
- Search index 생성이 간단하고 가벼움
- Search 할 이웃의 개수를 알고리즘이 보장 (parameter : search_k)
- 파라미터 조정을 통해 acc/speed Trade-off 조절 가능
- 학습하는 모델이 아니기 때문에 기존에 생성된 binary tree에 새로운 데이터 추가 불가

