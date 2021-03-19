# 3. 몽고DB 기본

---

👉 강의: 인프런 - [[NoSQL DB (몽고DB/mongodb) 기본부터 파이썬/데이터분석 활용까지!]](https://www.inflearn.com/course/nosql-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%AA%BD%EA%B3%A0db-%EC%9E%94%EC%9E%AC%EB%AF%B8%EC%BD%94%EB%94%A9/dashboard)

👉 발제자: 노연수 (2021.03.20)

---

# 3.1 MongoDB 다뤄보기 - robo 3T 설치

## Robomongo 설치

- [https://robomongo.org/download](https://robomongo.org/download)에서 Robo 3T 다운로드 후 설치
- MongoDB 실행

```bash
# Windows
net start MongoDB
net stop MongoDB
```

- Connect

*AWS 사용할 경우에는 ip주소 입력하여 Connect

---

# 3.2 MongoDB 다뤄보기 - Database와 Collection 만들기

## Create Database

- server name 우클릭 → Create Database → Database 이름 입력

## Delete Database

- database name 우클릭 → Drop Database

## Create Collection

- database name 우클릭 → Create Collection → Collection 이름 입력

## Delete Collection

- collection name 우클릭 → Drop Collection

## Insert Document

- collection name 우클릭 → Insert Document → Json 형태의 데이터 입력 → Save

    ![3%20%E1%84%86%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A9DB%20%E1%84%80%E1%85%B5%E1%84%87%E1%85%A9%E1%86%AB%20f928bf0deac445e9888de9d29957f545/Untitled.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1d558495-4803-4ac6-ae99-eb0fe0f8752f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T181031Z&X-Amz-Expires=86400&X-Amz-Signature=eceace326c907f412898739aebf9cd2f41ca9be1a40c46545b5c3a2966eaa420&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

- collection name 우클릭 → View Documents
- 인덱스 자동 생성

    ![3%20%E1%84%86%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A9DB%20%E1%84%80%E1%85%B5%E1%84%87%E1%85%A9%E1%86%AB%20f928bf0deac445e9888de9d29957f545/Untitled%201.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6453a786-f8b8-453c-a59e-e6b9cddcd8b6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T181100Z&X-Amz-Expires=86400&X-Amz-Signature=90399c106e0f5f55d81872471aa18b1fef895417fd7db0d5c137d4e4fa3afaf0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

## Delete Document

- document name 우클릭 → Delete Document
- collection name 우클릭 → Remove All Documents

---

# 3.3 SQL과 MongoDB 간단 비교 - MongoDB shell 익히기

- server name 우클릭 → Open Shell

```bash
# 전체 데이터베이스 열람
$ show dbs

# 데이터베이스 선택
$ use {DB 이름}
예) use mydb

# 선택된 데이터베이스의 콜렉션 열람
$ show collections

# collection 내 데이터 찾는 명령어
# find 인자가 없으면 전체 document 검색
$ db.{collection 이름}.find()

# db의 통계 정보 확인 (db, collections, 저장 공간 등)
$ db.stats()

# collection 생성
$ db.createCollection("{collection 이름}")
# capped:true 최초 제한된 크기로 생성된 공간에서만 데이터를 저장하는 설정 
# 넣을 때마다 저장 공간 추가 x ->고성능
# 일정 시간 저장하는 로그에 적합
$ db.createCollection("{collection 이름}", {capped:true, size:10000})

# capped 여부 알아보기
$ db.{collection 이름}.isCapped()

# collection 삭제
$ db.{collection 이름}.drop()

# collection의 통게 정보 확인
$ db.{collection 이름}.stats()

# collection 이름 변경
$ db.{collection 이름}.renameCollection("{변경할 collection 이름}")
```

---

# 3.4 몽고DB 데이터 입력 - SQL과 비교

## CRUD 명령

- Create (Insert)
- Read (Search)
- Update
- Delete (Drop)

## MongoDB collection 생성/변경

![3%20%E1%84%86%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A9DB%20%E1%84%80%E1%85%B5%E1%84%87%E1%85%A9%E1%86%AB%20f928bf0deac445e9888de9d29957f545/Untitled%202.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/91e21471-96c3-4101-95b8-b3adb2a543de/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T181128Z&X-Amz-Expires=86400&X-Amz-Signature=f3ba21404575cac82bc2c9274266e6c3b71eac0ec63e6d1ff397c36ccc3f8334&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

- **collection 생성**
    - Schema 따로 설정할 필요 x
    - PRIMARY KEY 설정 필요 x → document마다 id가 자동 생성되어 PK 역할을 한다
- **collection 구조 변경**
    - SQL: ALTER TABLE
    - MongoDB: 각각의 Document가 각각의 구조를 갖는다
- **기존 Document에 컬럼과 컬럼값 추가**
    - SQL: ALTER TABLE people ADD COLUMN join_date DATETiME
    - MongoDB: db.people.updateMany({ }, { $set: {join_date: new Date() } })
- **기존 Document에 컬럼과 컬럼값 삭제**
    - SQL: ALTER TABLE people DROP COLUMN join_date
    - MongoDB: db.people.updateMany({ }, { $unset: { "join_date": "" } })

## Document 입력

- `InsertOne`: 한 개의 document 생성
- `InsertMany`: list of document 생성

```bash
# document 입력 문법
$ db.users.insertOne(
	{
		name: "sue"
		age: 26,
		status: "pending"
	}
)
$ db.articles.insertMany(
   [
     { subject: "coffee", author: "xyz", views: 50 },
     { subject: "Coffee Shopping", author: "efg", views: 5 },
     { subject: "Baking a cake", author: "abc", views: 90  },
     { subject: "baking", author: "xyz", views: 100 },
     { subject: "Café Con Leche", author: "abc", views: 200 },
     { subject: "Сырники", author: "jkl", views: 80 },
     { subject: "coffee and cream", author: "efg", views: 10 },
     { subject: "Cafe con Leche", author: "xyz", views: 10 },
     { subject: "coffees", author: "xyz", views: 10 },
     { subject: "coffee1", author: "xyz", views: 10 }
   ]
)
```

![3%20%E1%84%86%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A9DB%20%E1%84%80%E1%85%B5%E1%84%87%E1%85%A9%E1%86%AB%20f928bf0deac445e9888de9d29957f545/Untitled%203.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aecc9788-2f42-4469-a111-d24642c9e78e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T181149Z&X-Amz-Expires=86400&X-Amz-Signature=ec816c80dc538062111013bbaa586f9d2818804b4cd3f994954b6698f66634fa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

---

# 3.5 몽고DB 데이터 읽기 - SQL과 비교1

## Document 읽기(검색)

- `findOne`: 매칭되는 한 개의 document 검색
- `find`: 매칭되는 list of document 검색

```bash
# document 읽기(검색) 문법
$ db.users.find(
	{ age: { $gt: 18 } },
	{ name: 1, address: 1 }
).limit(5)

# SELECT * FROM people
$ db.people.find() 

# SELECT _id, user_id, status FROM people
$ db.people.find({ }, { user_id: 1, status: 1 })

# SELECT user_id, status FROM people
$ db.people.find({ },{ user_id: 1, status: 1, _id: 0 })

# SELECT * FROM people WHERE status = "A"
$ db.people.find({ status: "A" })

# SELECT * FROM people WHERE status = "A" AND age = 50
$ db.people.find({ status: "A", age: 50 })

# SELECT * FROM people WHERE status = "A" OR age = 50
$ db.people.find({ $or: [ { status: "A" } , { age: 50 } ] })
```

---

# 3.6 몽고DB 데이터 읽기 - SQL과 비교2

## 비교 문법

- `$eq`: =, equal to
- `$gt`: >, greater than
- `$gte`: ≥, geater than or equal to
- `$in`: in
- `$lt`: <, less than
- `$lte`: ≤, less than or equal to
- `$ne`: ≠, not equal to
- `$nin`: not in

```bash
# SELECT * FROM people WHERE age > 25
$ db.people.find({ age: { $gt: 25 } })

# SELECT * FROM people WHERE age < 25
$ db.people.find({ age: { $lt: 25 } })

# SELECT * FROM people WHERE age > 25 AND age <= 50
$ db.people.find({ age: { $gt: 25, $lte: 50 } })

# SELECT * FROM people WHERE age = 5 or age = 15
$ db.people.find( { age: { $in: [ 5, 15 ] } } ))

# SELECT * FROM people WHERE user_id like "%bc%"
$ db.people.find( { user_id: /bc/ } )
$ db.people.find( { user_id: { $regex: /bc/ } } )

# SELECT * FROM people WHERE user_id like "bc%"
$ db.people.find( { user_id: /^bc/ } )
$ db.people.find( { user_id: { $regex: /^bc/ } } )

# SELECT * FROM people WHERE status = "A" ORDER BY user_id ASC                                           
$ db.people.find( { status: "A" } ).sort( { user_id: 1 } ) 

# SELECT * FROM people WHERE status = "A" ORDER BY user_id DESC
$ db.people.find( { status: "A" } ).sort( { user_id: -1 } )

# SELECT COUNT(*) FROM people
$ db.people.count()
$ db.people.find().count()
                                                 
# SELECT COUNT(user_id) FROM people
$ db.people.count( { user_id: { $exists: true } } )
$ db.people.find( { user_id: { $exists: true } } ).count()
                                                  
# SELECT COUNT(*) FROM people WHERE age > 30
$ db.people.count( { age: { $gt: 30 } } )
$ db.people.find( { age: { $gt: 30 } } ).count()
                                                  
# SELECT DISTINCT(status) FROM people
db.people.distinct( "status" )

# SELECT * FROM people LIMIT 1
db.people.findOne()
db.people.find().limit(1)
```

---

# 3.7 몽고DB 데이터 수정 - SQL과 비교

## Document 수정

- `updateOne`: 매칭되는 한 개의 document 업데이트
- `updateMany`: 매칭되는 list of document 업데이트
- `$set`: field 값 설정
- `$inc`: field 값 증가 또는 감소
    - 예) $inc: { age: 2 } → age 값 본래 값에서 2 증가

```bash
# Document 수정 문법
$ db.users.updateMany(
	{ age: { $lt: 18 } },
	{ $set: { status: "reject" } }
)

# UPDATE people SET status = "C" WHERE age > 25
$ db.people.updateMany( { age: { $gt: 25 } }, { $set: { status: "C" } } )

$ db.people.updateOne( { age: { $gt: 25 } }, { $set: { status: "C" } } )

# UPDATE people SET age = age + 3 WHERE status = "A"
$ db.people.updateMany( { status: "A" } , { $inc: { age: 3 } } )
```

---

# 3.8 몽고DB 데이터 삭제 - SQL과 비교

## Document 삭제

- `removeOne`: 매칭되는 한개의 document 삭제
- `removeMany`: 매칭되는 list of document 삭제

```bash
# Document 삭제 문법
$ db.users.deleteMany(
	{ status: "reject" }
)

# DELETE FROM people WHERE status = "D"
$ db.people.deleteMany( { status: "D" } )

# DELETE FROM people
$ db.people.deleteMany({})
```

---

# [참고] 파이썬 라이브러리 사용법 1, 2