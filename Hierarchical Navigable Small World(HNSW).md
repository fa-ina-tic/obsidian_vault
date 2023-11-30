robust algorithm which works especially well for large dataset vectors

construct such a graph where a path between any pair of vertices could be traversed in a small number of steps 

multi-layered graph with fewer connections on the top layers and more dense regions on the bottom layers

## Search
Starts from the highest layer
search nodes which is closest to query
if there's no nodes that is more close to query, go to lower layer

lowest layer has all node connection in there
nearest neighbor which is located in lowest layer would be the answer to the query

it has same problem with NSW(early stopping), and it can also improved by using several entry points

## Complexity
refers to [original paper](https://arxiv.org/pdf/1603.09320.pdf), the number of operations is bounded by a constant(The number of layer)
The number of all layers in a graph is logarithmic, so total search complexity would be $O(logn)$ 

## Construction 
Nodes in HNSW are inserted sequentially one by one.
Every nodes randomly assigned an integer l, which is the maximum layer that node locates.

$l$ selected randomly using $exponentially\;decaying\;probability\;distribution$ ([wikipedia](https://en.wikipedia.org/wiki/Exponential_distribution))normalized by the non-zero multiplier $mL$ ($mL=0$ results in a single layer in HNSW and non-optimized search complexity)

normally most of l values would be 0.
The larger values of $mL$ increases the probability of a node appearing on higher layers

$$l=float[-ln(uniform(0,1)) * m_L$$
![[Pasted image 20231128162812.png]]
**distribution of $l$ by $mL$**

> To achieve the optimum performance advantage of the controllable hierarchy, the overlap between neighbors on different layers (i.e. percent of element neighbors that are also belong to other layers) has to be small. — Yu. A. Malkov, D. A. Yashunin.

decreasing overlap and more traversals is in tradeoff relationship. So need to choose appropriate *mL* to balance both the overlap and the number of traversals

author of the paper propose choosing the optimal value of $mL$ which is equal to $1/ln(M)$. This value corresponds to the parameter $p=1/M$ of the skip list being an average single element overlap between the layers

## Insertions
Two phases left after a node assigned the value $l$ 
1. The algorithm starts from the upper layer and greedily finds the nearest node. The found node is then used as an entry point to the next layer and the search process continues. Once the layer $l$ is reached, the insertion proceeds to the second step
2. Algorithm insert new node from layer $l$ and greedily searches for $efConstruction$(hyperparameter) neighbors. $M$ out of $efCounstruction$ neighbours are chosen and edges to inserted node are built. It ends when edges are inserted on the lowest layer 0

## Choosing hyperparameter values
recommendation by original paper 
- good values for $M$ lie between 5 and 48. smaller would be better for lower recalls or low-dimensional data and bigger would be better for higher recalls or high-dimensional data
-  Higher values of $efConstruction$ imply a more profound search as more candidates are explored but requires more computations. Appropriate value of $efConstruction$ would have 0.95 - 1 of recall during training
- $M_{max}$ (maximum number of edges a vertex can have) recommended to be close to $2*M$. 

## Candidate selection heuristic
How to choose $M$ out of $efConstruction$. 
1. choosing closest M from candidates : Most naive way to choose $M$. can decrease searching speed
So heuristic approach invented by author
> The heuristic considers not only the closest distances between nodes but also the connectivity of different regions on the graph

it first build edge with closest node. And sequentially compare the distance between (new node and other node's distance) and (the closest node and other node's distance). only when new node's distance is closer than other distance build edge.

## Complexity
insertion of a single vertex imposes $O(logn)$ of time. total complexity is $O(n*logn)$ 

## Combining HNWS with other methods
HNWS can be used together with other similarity search methods for better performance. One of the most popular ways to do it is combining with an [[Inverted file index and product quantization]]($indexIVFPQ$)

HNWS will be a coarse quantizer for __indexIVFPQ__ and will be responsible for finding the nearest Voronoi partition so the search scope can be reduced

create HNSW index to all Voronoi centroids and find the nearest Voronoi centroid with query. After that, query vector is quantized within a respective Voronoi partition and distances are calculated by using PQ codes.

Using only and inverted file index limits to total number of Voronoi partition. if it is too large, searching nearest centroids(brute-force) would costs a lot. HNSW can help to use more numbers of Voronoi partition and searching nearest centroids
in other world, if Voronoi partition don't have to be many(256 or 1024), HNSW would not bring any significant benefits and only use memory to store the graph structure

>That is why when merging HNSW and inverted file index, it is recommended to set the number of Voronoi centroids much bigger than usual. By doing so, the number of candidates inside each Voronoi parition becomes much smaller

The number of candidates would be smaller than only using inverted index, so searching inside respective Voronoi partition would be much cheaper




based theory
based structure
- [[Skip lists]]
- [[NSW]]

