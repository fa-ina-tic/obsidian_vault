
vector search 성능평가 지표
- accuracy
- speed

## Service
- [[elasticsearch]]

## Library
- Facebook AI Similarity Search (FAISS)
	- base algorithm : HNSW
- [[Lucene]]

## vector similarity search algorithm
- k-Nearest Neighbors(k-NN)
- Ball Tree
- KD-Tree
- Scalable Nearest Neighbors (ScaNN)
	- step
		1. vectorizing
		2. indexing - [[Locality Sensitive Ranking(LSH)]]
		3. refinement - [[Optimal Transport]]
		4. ranking
	- supported distance metric
		1. Euclidean(L2) distance
		2. cosine similarity
		3. inner product similarity
- ANN
	- [[Approximate Nearest Neighbors Oh Yeah(ANNOY)]]
	- [[NSW]]
		- [[Hierarchical Navigable Small World(HNSW)]]





## vector search method
- hybrid search
- Reciprocal rank fusion

ApproxRetrievalStrategy
hybrid -> add a 