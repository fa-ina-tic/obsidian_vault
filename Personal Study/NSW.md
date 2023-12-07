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

## Prob
early stopping
![[Pasted image 20231128111227.png]]
-> 여러 Entrypoint를 사용하는 것으로 개선 가능 -> 시간 복잡도는 k배 증가(k=사용 entrypoint 개수)

## Construction
![[Pasted image 20231128111621.png]]
shuffle dataset points and inserting them one by one to current graph
new node linked by edges to the $M$ nearest vertices

long-range edges will likely be created at the beginning phase of the graph construction. They play an important role in graph navigation

having long range connection makes query searching faster --> main concept of [[Hierarchical Navigable Small World(HNSW)]]