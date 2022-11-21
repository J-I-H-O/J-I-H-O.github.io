## 1. EleaticSearch란?
Apache Lucene 기반의 Java 오픈소스 분산 검색엔진.

<br>

## 2. ElasticSearch의 특징

### 분산 처리
- 분산 시스템 구성으로 대량의 데이터를 병렬적으로 다룰 수 있으므로 빠른 처리가 가능함.
- 분산 환경에서 데이터를 Shard 라는 단위로 쪼개어 저장함.

### Near Real-Time
- 분산 처리를 통해 거의 실시간(Near Real-Time)에 데이터 검색 가능. 
- 내부적으로 commit과 flush 등의 과정을 거치므로, 완전 실시간(Real-Time)은 아님.

### 대량의 비정형 데이터 보관 및 검색 가능
- 기존의 관계형 데이터베이스로 처리하기 어려운 대량의 `비정형 데이터` 검색 가능.

> 비정형 데이터(unstructured data)

> 미리 정의된 데이터 모델이 없거나 미리 정의된 방식으로 정리되지 않은 정보.
> 즉, 정해진 규칙이 없어서 값의 의미를 쉽게 파악하기 힘든 데이터. 
> 음성, 영상과 같은 데이터가 비정형 데이터에 속함.

### 스키마리스(Schemaless)
- 기존의 는 자료의 구조, 표현 방법, 자료간의 관계등을 정의한 Schema에 따라 데이터를 적합한 형태로 변경하여 저장 및 관리하지만, ElasticSearch는 비정형의 다양한 형태의 문서도 자동으로 색인, 검색이 가능

### 전문 검색(Full-text Search)
- 내용 전체를 색인화해서 특정 단어가 포함된 문서를 검색할 수 있음

### RESTful API
- HTTP 통신 기반의 RESTful API를 사용하고, 요청과 응답으로 JSON을 활용하므로 개발 언어와 운영체제 등의 시스템에 국한되지 않은 다양한 플랫폼에서 응용이 가능함.

### 역색인(Inverted Index)
- 각 문서에서 추출된 Term들과 Documents의 관계를 나타낼 때 `Inversted Index` 방식을 사용하기 때문에 속도의 큰 저하 없이 빠른 속도로 검색이 가능함.

> `기존의 Index` : 어떤 Document에 어떤 Term이 포함되는지 나타냄
> 
> `Inverted Index` : 어떤 Term들이 어떤 Document에서 나타나는지 Term이 등장한 Document id를 나타냄.

> <p align="center"><img src="https://i.stack.imgur.com/iGri3.png"> 
> Inverted Index 예시</p>

### 통계 분석
- 비정형 로그 데이터를 수집하고 한 곳에 모아 통계 분석이 가능함. Kibana를 통해 데이터를 시각화하고, 모니터링 할 수 있음.

### Transaction, Rollback 등의 기능을 제공하지 않음
- 분산 시스템으로 구성되어있어 전체적인 클러스터의 성능 향상을 위해 시스템적으로 비용 소모가 큰 트랜잭션과 롤백을 지원하지 않음.

### 데이터의 업데이트를 제공하지 않음
- UPDATE 명령시 데이터를 삭제했다가 새로운 문서를 생성함. 많은 비용을 소모하지만, 이를 통해 불변성(Immutable)을 제공함.

<br>
## Reference
https://velog.io/@jakeseo_me/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-2-DB%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84

https://jaemunbro.medium.com/elastic-search-%EA%B8%B0%EC%B4%88-%EC%8A%A4%ED%84%B0%EB%94%94-ff01870094f0

