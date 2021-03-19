# 1. NoSQL 이해

---

👉 강의: 인프런 - [[NoSQL DB (몽고DB/mongodb) 기본부터 파이썬/데이터분석 활용까지!]](https://www.inflearn.com/course/nosql-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%AA%BD%EA%B3%A0db-%EC%9E%94%EC%9E%AC%EB%AF%B8%EC%BD%94%EB%94%A9/dashboard)

👉 발제자: 노연수 (2021.03.20)

---

# 1.1 빅데이터와 NoSQL 이해

## 빅데이터

- 기존: 관계형 데이터베이스 (RDBMS)
    - SQL 언어로 사용 가능
    - SQL 데이터베이스
- 빅데이터는 기존의 관계형 데이터베이스로 처리하기 어려운 부분 존재
- 빅데이터: NoSQL 데이터베이스 (Not only SQL, SQL보다 좀 더 기능이 많다!)

## NoSQL (Not only SQL)

- SQL은 저장할 데이터의 규격을 미리 만들어야 한다 → 저장하고 싶은 데이터를 늘리고 싶을 때 규격을 새로 업데이트
- 이러한 RDBMS의 한계 극복을 위해 만들어진 새로운 형태의 데이터 저장소가 NoSQL
- 고정된 스키마 및 JOIN 존재 X

### 💡SQL vs. NoSQL

![1%20NoSQL%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%20696399321788434aace237b1e9458201/Untitled.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5688166c-f202-43d5-bfb2-49aebc83e644/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T180746Z&X-Amz-Expires=86400&X-Amz-Signature=d841f66a3c9b0a89e9b39f6c9f85233641351b83ef5949dc6a607cbdfdcaf3b9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

---

# 1.2 NoSQL의 대표적인 데이터베이스 mongodb 소개

### ❓Why NoSQL?

- NoSQL은 빅데이터를 다루는 데에 있어 성능 면에서 개선이 있다
- RDBS는 read를 주로 할 때는 성능이 나쁘지 않지만, write의 비중이 늘어나면 성능이 저하되거나 불안정
- 초당 데이터가 수십만개씩 쌓이는 서비스가 많아지는 경우(SNS, 온라인 서비스 등) NoSQL이 유리
- NoSQL 데이터베이스는 각기 데이터베이스를 다루는 인터페이스가 다르다
    - Key/Value Store
    - Wide Column Store
    - Document Store
    - Graph Store

    ![1%20NoSQL%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%20696399321788434aace237b1e9458201/Untitled%201.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6678cba3-1cdd-4f21-8df5-fed747303f42/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T180843Z&X-Amz-Expires=86400&X-Amz-Signature=e313e84072b5e77a4b0115c98aa3d6d2d1f92cade33643bed40496a2cb0edf0c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

## mongoDB

- document db
    - JSON 기반 데이터 관리
    - JSON document = { "id":"01", "languange":"java", "edition": { "first": "1st", "second":"2nd", "third":"third" } }
- mongoDB document 예)

    ```json
    {
        "_id": ObjectId("5099803df3f42312312391"),
        "username": "davelee",
        "name": { first: "Dave", last: "Lee" }
    }
    ```

---

# 1.3 mongodb 데이터 구조와 관련 용어 정리

## MongoDB 데이터 구조

- Database - Collection - Document
- Database는  Collection의 집합
- Collection은 Document의 집합
- Collection은 RDBMS의 Table과 유사한 개념이나 Schema 정의 x
- Collection에 JSON 형태의 Document를 넣는다
- RDBMS: Database - Table - Data

    → 데이터베이스 안에 테이블이 있고, 각각의 테이블마다 데이터가 있으며, 테이블 간 관계가 있다. 

![1%20NoSQL%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%20696399321788434aace237b1e9458201/Untitled%202.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/be21720b-d87f-4ab1-ab49-ffa6bf131d5d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T180909Z&X-Amz-Expires=86400&X-Amz-Signature=02c3d77ae7c3f6e49107ef615bc546d867127a7efd4d1d8059ba8d583d8fdca1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

![1%20NoSQL%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%20696399321788434aace237b1e9458201/Untitled%203.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/90f9fdc2-51d6-4ad7-8f21-ed27d75da7f6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T180927Z&X-Amz-Expires=86400&X-Amz-Signature=63bbdc99503ae2e810c279971a005f9aa6149480ca11ec0cc27d61d8d2aa861e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)