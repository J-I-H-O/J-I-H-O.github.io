---
categories: [ElasticSearch]
---

<p><img src="https://velog.velcdn.com/images/sjh9391985/post/6d455887-f18f-4ff7-ac52-598d4f079239/elasticsearch.png"></p>

## 1. ElasticSearch와 관계형 데이터베이스

<p><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99E0A9425C98CF7A0A"></p>
관계형 데이터베이스와 ElasticSearch는 위와 같이 대응시킬 수 있음

## 2. ElasticSearch 아키텍처와 용어

<p><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99A97A355C98D42D2E"></p>

### 클러스터(Cluster) 
- ElasticSearch에서 가장 큰 시스템 단위. 하나 이상의 노드로 이루어진 노드들의 집합
- 서로 다른 클러스터는 데이터의 접근, 교환을 할 수 없는 독립적인 시스템으로 유지되며, 여러대의 서버가 하나의 클러스터를 구성할 수 있고, 한 서버에 여러대의 클러스터가 존재할 수도 있음

### 노드(Node)
- ElasticSearch를 구성하는 하나의 단위 프로세스. Cluster를 이루는 요소.
- 여러개의 노드로 구성된 ElasticSearch 서버는 부하를 여러개의 서버가 같이 부담하므로 수평적으로 데이터가 커질 수 있음.
- 역할에 따라 Master, Data, Ingest, Coordinating 노드로 구분
  - 마스터 노드(Master Node)
    - 클러스터 관리
    - 노드 추가/제거 등 클러스터의 전반적 관리를 담당
  - 데이터 노드(Data Node)
    - 실질적인 데이터 저장. 데이터가 실제로 분산 저장되는 물리공간인 샤드(Shard)가 배치됨
    - 검색과 통계 등 데이터 관련 작업 수행. 
  - 코디네이팅 노드(Coordinating Node)
    - 사용자의 요청만 받아서 처리함. 단순히 요청을 `Round Robin` 방식으로 분산시켜주는 노드
    - 클러스터 관련 요청은 마스터 노드로, 데이터 관련 요청은 데이터 노드로 전달함
  - 인제스트 노드(Ingest Node)
    - Document의 전처리를 담당함
    - 인덱스 생성 전 문서의 형식을 다양하게 변경할 수 있음 

### Index
- 관계형 데이터베이스에서의 Database와 table과  대응되는 개념
- 데이터 저장 공간
- 하나의 물리 노드에 여러개 논리 인덱스 생성

### Shard
- Sharding은 데이터를 분산해서 저장하는 방법을 의미함.
- ElasticSearch에서 Scale out을 위해 인덱스를 여러 파티션으로 쪼갠 것.
  
### Replica
- 노드가 손실되었을 경우 데이터의 신뢰성 보장을 위해 샤드들을 복제한 것.
- 따라서 Replica는 Shard와 서로 다른 노드에 존재할 것을 권장함.

<p><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F991563425C98CB341A"></p>

- 위의 그림에서 Shard3를 저장하고있는 Node2에 Failure가 발생하더라도 Node3에서 Replica3를 얻어낼 수 있음.

### Document
- 관계형 데이터베이스의 Row에 대응됨
- 데이터가 저장되는 최소 단위
- JSON 포맷으로 저장

### Field
- 관계형 데이터베이스의 Column에 대응됨
- 문서를 구성하기 위한 속성
- 하나의 필드는 목적에 따라 다수의 데이터 타입을 가질 수 있음
  - 예를들어 한국어 필드에 대해 초성 필드 추가..?
  
### Mapping
- 문서의 필드, 필드 속성을 정의하고 그에 따른 색인 방법을 정의하는 프로세스
- 스키마 정의 프로세스라고 볼 수 있음

<br>
<hr/>
<br>

## Reference
https://victorydntmd.tistory.com/308

https://velog.io/@jakeseo_me/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-3-%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%9A%A9%EC%96%B4-%EB%B0%8F-%EA%B0%9C%EB%85%90-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0

<br>
<hr/>
<br>

<script src="https://utteranc.es/client.js"
        repo="J-I-H-O/J-I-H-O.github.io"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>