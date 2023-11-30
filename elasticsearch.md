distributed document store based on [[Lucene]]

- provides:
	- REST API
	- distributed computing and scale out(sharding)
	- Stability(replica shard, translog)

## index 구조
![[Pasted image 20231124133851.png]]
$$Elastic Search index \supset shard \supset lucene index \supset segment \supset document$$
### Shard
Elasticsearch가 도입한 개념. index 안의 많은 document를 여러 곳에 분산시켜 서버의 수평적 확장(=scale out) 가능
관리자
1. ./index
	1. [[Lucene]]이 관리
	2. 색인된 문서가 반영구적으로 저장되는 공간
	3. 세그먼트가 저장되는 공간
2. ./translog
	1. 장애 발생 시 데이터 유실을 방지하기 위해 [[elasticsearch]]가 도입한 방식
	2. 문서 색인 직후 세그먼트가 바로 생성되는 것이 아니라 translog와 메모리 버퍼에 먼저 기록
	3. [[Lucene]]이 디스크에 물리적으로 기록하기 전에 장애 발생 시 translog 기록을 보며 데이터 복구 가능
	4. flush API 호출 시 trasnlog 내용 삭제. 

### Segment
- [[Lucene]]이 관리하는 개별적인 색인.
- [[elasticsearch]] search index의 데이터는 segment라는 각각의 조각조각으로 구성되어 있음
- 검색 시 세그먼트 하나하나를 조회한 후 그 결과를 병합에 리턴
- 한 세그먼트에 단일 파일이나 여러 파일로 구성 가능
- 한 세그먼트를 다중 색인 파일로 구성

### 색인파일 구성

| file    | description                       |
| ------- | --------------------------------- |
| \_0.si  | 0번 세그먼트의 메타데이터         |
| \_0.cfs | 0번 세그먼트에서 자주 쓰는 엔트리 |
| \_0.cfe | 0번 세그먼트의 모든 엔트리 테이블 |
| segments_N        | 모든 세그먼트 참조를 보관하는 메타파일. 색인을 열 때 가장 먼저 읽는다.N=커밋횟수

위의 표 이외에도 많은 Index 파일 존재하며, 아래와 같이 유기적으로 연결되어 있음
![[Pasted image 20231129102635.png]]

### Document
input data
key=term인 inverted index 구조로 segment 내부에 존재
indexed document contents stored in segment with a form of binary file
