---
categories: [ElasticSearch]
---

<p><img src="https://velog.velcdn.com/images/sjh9391985/post/6d455887-f18f-4ff7-ac52-598d4f079239/elasticsearch.png"></p>

## 1. 왜 ElasticSearch를 사용하는가?

### DB 뿐만 아니라 검색엔진을 도입하는 이유

RDBMS도 데이터 저장 뿐만아니라 SQL를 이용하여 조건에 맞는 데이터에 대한 검색도 수행할 수 있지만, 아래와 같은 이유로 검색엔진을 도입한다. 

1. 관계형 데이터베이스는 단순 텍스트 매칭에 대한 검색만을 제공
2. ElasticSearch에서는 텍스트를 여러 단어로 변형하거나 텍스트의 특질을 이용한 동의어나 유의어를 활용한 검색 가능
3. 관계형 데이터베이스에서 불가능한 비정형 데이터의 색인과 검색이 가능
4. 형태소 분석을 통한 자연어 처리 가능
5. 역색인(Inverted Index)을 통한 빠른 검색 가능

## 2. Elastic Stack
<p><img src="https://velog.velcdn.com/images%2Fshinychan95%2Fpost%2F693812e1-58c0-42c2-a5a8-5eb59ff050c2%2Fimage.png"></p>

- ElasticSearch : 대규모의 데이터 저장, 쿼리, 검색, 분석 등 모든 처리를 담당
- Kibana : 데이터 시각화 및 분석을 위한 클라이언트 도구
- Beats, Logstash : 
  - Logstash : 다양한 플러그인을 이용하여 데이터 집계 및 보관, 서버 데이터 처리, 파이프라인으로 데이터를 수집하여 필터를 통해 변환 (ETL) 후 ElasticSearch로 전송함. 데이터 소스가 있는 모든 장비에 설치해야 함. 
  - Beats : Logstash와 비슷하나, 변환 기능이 제외되어 있어 보다 가볍게 사용 가능함.

## 3. 대략적인 동작 방식

<p><img src="https://velog.velcdn.com/images%2Fshinychan95%2Fpost%2F03b81cc9-b93c-48f5-be84-e18d9d2336e9%2Fimage.png"></p>

- 특정 서버에서 생성되는 데이터를 RDBMS 또는 Non-RDBMS에 저장하고, 검색 혹은 분석이 필요한 부분만을 데이터로 추출하여 ElasticSearch에 자동 저장시킴
- 이때 Elastic stack의 `logstash`가 기존의 DB에서 ElasticSearch로 자동 저장하는 `ETL` 기능을 수행함

> ETL (Extract, Transform, Load)
>
> 한 곳에 저장된 데이터를 필요해 의해 형태를 변형하여 재적재하는 과정
> https://itholic.github.io/etl/


<br>
<hr/>
<br>

## Reference
https://velog.io/@jakeseo_me/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-2-DB%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84#db%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84

https://velog.io/@shinychan95/Elasticsearch-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-%EB%B0%8F-%ED%8A%B9%EC%A7%95-%EC%A0%95%EB%A6%AC

https://velog.io/@jakeseo_me/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-2-DB%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84#db%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84

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