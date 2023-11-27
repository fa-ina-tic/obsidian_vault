공간상의 벡터들을 배치하고 이들을 적절하게 연결하여 벡터 간 탐색 가능하도록 만드는 알고리즘

time complexity : O($log^kN$)
greedy routing 사용
Routing : low-level vertices 에서 탐색을 시작해서 high-level vertices에서 종료되는 것을 뜻함.

low-level vertices에서는 연결이 적기 때문에 빠르게 가장 가까운 neighbor가 어딘지를 탐색하고, 아래로 내려갈수록 더 정확하게 가까운 neighbor가 어딘지를 탐색합니다.

## Search
- greedy algorithm
- Entry point 랜덤 지정
- entry point 의 근접 벡터 중에서, query vector에 가장 근접한 벡터로 이동.
- 현재 소속된 노드보다 쿼리 벡터에 가까운 노드를 찾지 못하면 search 멈춤
- 
