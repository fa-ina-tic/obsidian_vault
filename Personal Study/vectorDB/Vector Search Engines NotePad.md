
## vector search 성능평가 지표
- accuracy
- speed

## Related Hypothesis
[[Manifold Hypothesis]]
위의 가설을 토대로 고차원의 데이터(자연어, 이미지 등등)을 유의미한 정보를 가지는 벡터로 변환하고, 유사한 의미를 가지는 경우 유사한 벡터값을 가진다는 가정하에 진행된다.

## Service(Vector DB & Vector search)
- [[elasticsearch]]
- pinecone
- milvus
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
- [[ANN]]
	- [[Approximate Nearest Neighbors Oh Yeah(ANNOY)]]
	- [[NSW]]
		- [[Hierarchical Navigable Small World(HNSW)]]
			- related hypothesis : [[Six Handshake Rules]]





## vector search method
- vector similarity search
- hybrid search
	- Reciprocal rank fusion

ApproxRetrievalStrategy
hybrid -> add a 