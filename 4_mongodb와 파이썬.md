# pymongo로 CRUD 해보기

## 0. pymongo로 db connect하기

아나콘다 환경일 경우 conda를 사용하시면 됩니다.
아니면 pip를 씁시다.

```python
pip install pymongo
conda install pymongo
```

일단 pymongo로 db가 있는 컴퓨터에 연결을 합니다. 연결되는 디폴트 포트는 27017 포트입니다. 몽고디비의 기본 연결 포트입니다.
```python
conn = pymongo.MongoClient()
conn = pymongo.MongoClient('mongodb://cloud computer 주소')
```
MongoClient의 괄호 안에 mongodb:// 치고 ip주소를 넣으면 해당 aws주소의 27017 포트로 연결됩니다. 

parameter를 다음과 같이 사용할 수도 있습니다.
```python
conn = pymongo.MongoClient(host='mongodb://cloud computer 주소',port=11111,username='jihoon',password='123123')
```
이렇게 파라미터를 넣어줘서 포트 설정을 다르게 할 수 있고 연결되는 pc에서 요구하는 authentification을 만족시킬 수도 있습니다.
자세한 api 명세는 [링크](https://pymongo.readthedocs.io/en/stable/api/pymongo/mongo_client.html)에서 확인 하실 수 있습니다. pymongo 공식 문서입니다.

```python
print(conn.list_database_names())
```
이 명령어를 치면 pc에 있는 데이터베이스의 리스트를 확인 할 수 있씁니다. 


이제 Mongodb서버가 있는 컴퓨터를 지칭하는 객체를 변수로 저장했습니다. 그럼 이제 mongodb database를 지칭하는 객체를 만들어 봅시다.

```python
db=conn.{db이름}
```
이렇게 기존 database에 접근하거나 또는 새로운 database를 지정할 수 있습니다.

데이터베이스 까지 접근 했으니 이제 NoSQL에서 테이블의 역할을 하는 Collection에 접근할 차례입니다.
```python
collect = db.{collection이름}
```
이런 식으로 기존 콜렉션을 불러오거나 새로운 콜렉션을 만들어 줍니다.

<span style="color:red; font-size:2em">여기서 잠깐!!</span>

만약 데이터 베이스를 새로 만들거나 collection을 새로 만들때 insert나 update 명령어를 써서 새로운 데이터를 실제로 넣기 전까지는 데이터베이스나 콜렉션이 만들어지지는 않습니다. 즉 실제 데이터(document)가 삽입이 되어야지 기존에 선언만 되어있었던 db,collection이 실제로 만들어 집니다.

## 1. CREATE
pymongo에서 create를 하는 명령어는 insert_one,insert_many가 있습니다.
mongo shell에서 쓰던 insertOne()과 pymongo의 insert_one은 동일한 명령어 입니다.

```python
post = {"author": "Mike", "text": "My first blog post!", "tags": ["mongodb", "python", "pymongo"] }

{collection을 지칭하는 변수}.insert_one(post)
```
이런 식으로 insert_one을 쓸 수 있습니다.

다음으로 여러 document를 한번에 삽입하는 insert_many를 살펴 보겠습니다.
```python
{collection 지칭하는 변수}.insert_many(
    [
        { "author":"Dave Ahn", "age":25 },
        { "author":"Dave", "age":35 }
    ]
)
```
이렇게 list화 시켜서 insert_many의 parameter로 넣어주면 됩니다.

## 2. READ
이제 데이터를 DB에서 읽어오는 메소드를 알아 보겠습니다.
insert와 마찬가지로 find_one(), find 메소드가 존재합니다. 두 함수 모두 조건을 추가하는 방법은 동일합니다.

```python
{collection 지칭하는 변수}.find(
        { "author":"Dave Ahn"})
{collection 지칭하는 변수}.find_one(
        { "author":"Dave Ahn"})
```
이렇게 parameter로 dict형식으로 조건을 추가해주면 해당 조건을 만족하는 document만 READ됩니다.

find_one메소드의 경우에 같은 조건인 document가 여러개 있을때 제일 첫번째 document를 리턴합니다.

find_one의 경우 document가 하나만 리턴 되기 때문에 리턴값이 document로 전달 됩니다. 하지만 find는 여러 document가 리턴되기 때문에 iterable한 객체 형식은 Cursor형식으로 리턴 됩니다. 이러한 iterable한 객체는 for문을 이용해 document하나씩 확인 할 수 있습니다.

```python
for doc in {collection 객체}.find():
    print(doc)
```
이런 식으로 할 경우 모든 document를 확인 할 수 있습니다.

여기에 덧붙여 find로 가져온 document들을 특정 조건으로 sort할 수 있습니다.

```python
for doc in {collection 객체}.find().sort("age"):
    print(doc)
```
이 경우에는 find로 불러온 객체의 age필드의 값을 바탕으로 sort가 된 document들을 볼 수 있습니다.

추가적으로 컬렉션에 있는 데이터의 수를 알 수 있는 메소드로 count_documents가 있습니다.  역시 다른 메소드들과 같이 컬렉션 변수 뒤에 메소드 변수로 쓰면 됩니다. 또한 parameter로 제한 조건을 둘 수 있습니다. 다음 예시를 보겠습니다.

```python
{collection 지칭하는 변수}.count_documents(
        { "author":"Dave Ahn", "age":25 })
```
이러면 author이 Dave Ahn인 사람과 age가 25인 document만 count된 결과가 도출 됩니다.
참고로 이전 버전에서 가능하던 .count()메소드는 depreciated되었습니다. 안쓰는걸 추천합니다.

## 3. UPDATE
기존의 document를 변경하는 update에 대해서도 알아 보겠습니다. update도 다른 CRUD 명령어 처럼 update_one, update_many 메소드 두개로 이루어져 있습니다.

```python
{collection 객체 변수}.update_one( { "author" : "Dave" }, 
    { "$set" : 
        { "text" : "Hi Dave" }
    }
)

{collection 객체 변수 }.update_many( { "author" : "Dave" }, 
    { "$set" : 
        { "age" : "40" }
    }
)
```
이렇게 parameter로 update할 document를 선별하는 조건, update 방식을 차례대로 넣으면 됩니다. 위의 경우 첫번째 코드는 author가 Dave인 경우 text필드를 Hi Dave로 바꾸는 명령어 입니다. 여기서 $set는 shell에서의 set와 같습니다. set은 필드값을 설정할 때 사용되는 명령어 입니다.

여기서 우리가 하나 알아야 할 것은 만약 set으로 지정한 필드가 없을 경우 CREATE와 같이 새로운 필드가 생성된다는 겁니다.

앞에서 나타난 find,insert와 같이 update_one의 경우 하나의 document만 변경되고 update_many는 모든 조건을 만족하는 Document들을 수정합니다.


## 4. DELETE

역시 delete도 마찬가지입니다.
delete_one, delete_many 메소드가 존재합니다.

```python
{collection 객체 변수}.delete_one( {"author":"Dave Lee"} )

{collection 객체 변수}.delete_many( {"author":"Dave Lee"} )
```

delete_one의 경우 해당하는 document 1개가 삭제되는 반면
delete_many는 해당하는 document 모두가 삭제됩니다.

또한 delete_many의 parameter로 아무것도 주지 않을 경우 collection의 모든 document들이 삭제되니 조심하셔야합니다.


# 출처
1. https://pymongo.readthedocs.io/en/stable/api/pymongo/mongo_client.html
2. https://somjang.tistory.com/entry/MongoDB-Python과-Pymongo를-활용하여-데이터-추가하고-출력해보기
3. https://basketdeveloper.tistory.com/40
4. Nosql DB 기본부터 파이썬/데이터분석 활용까지