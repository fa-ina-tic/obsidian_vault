
vector search 성능평가 지표
- accuracy
- speed


거리 기반 top k vector search
old-fashioned
- k-Nearest Neighbors(k-NN)
- Ball Tree
- KD-Tree

new
- Facebook AI Similarity Search (FAISS) 
- Scalable Nearest Neighbors (ScaNN)
	- step
		1. vectorizing
		2. indexing - [[Locality Sensitive Ranking(LSH)]]
		3. refinement - [[Optimal Transport]]
		4. ranking
	- supported distance metric
		1. Euclidean(L2) distance
		2. cosine distance
		3. inner product similarity

