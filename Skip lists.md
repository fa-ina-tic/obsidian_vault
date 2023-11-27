Data structure that can be used as algorithm.
randomized algorithm

probabilistic data structure that allows inserting and searching elements within a sorted list for O(logn) on average

skip list is constructed by several layers of linked lists. The lowest layer has the original linked list with all the elements in it.

moving to higher level -> skipped elements increases & decreasing the number of connections

search procedure
- starts from highest level
- 레이어의 찾으려는 값이 다음 element보다 크다면 아래 레이어로 내려감
- binary search tree에서 완하는 값을 찾는 과정과 비슷함