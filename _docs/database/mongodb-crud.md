---
title: MongoDB CRUD
tags: 
 - show
 - use
 - find
 - findOne
 - pretty
 - insert
 - insertMany
 - update
 - updateMany
 - deleteOne
 - drop


description: Learn about the basic jargons of database!
---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->

# MongoDB CRUD
`MongoDB`를 통해서 CRUD를 하는 방법을 알아보자.  

---

## READ

---

### show dbs
데이터베이스 리스트를 터미널에서 확인할 수 있다.

---

### use [database]
데이터베이스의 리스트에 나온 이름을 use하여 데이터베이스를 사용한다.  

### show collections
사용중인 데이터베이스의 컬렉션 리스트가 출력된다.  

### find
find 명령어를 이용해 일정 조건에 따라 데이터를 조회하는 방법과 조회한 데이터의 수를 세는 방법을 알아보자.  
```bash
db.zips.find({"state":"NY"})
```
이 명령어를 사용할 때 이미 필요한 데이터베이스 공간으로 이동했기 때문에,  
사용할 데이터베이스의 이름을 특정하여 작성하지 않는다.  
위 명령어에서 db는 이전에 `use`한 db를 가리킨다.  
<br>

명령어에 대한 결과는 JSON 형식으로 출력된다.  
이때 `find`명령어에 따른 실제 결과물은 랜덤하게 선택된 20개 결과물만 출력된다.  
해당 조건에 맞는 다음 20개의 도큐먼트를 조회하기 위해서는, iterate의 줄임말인 `it` 명령어를 사용해야 한다.  
<br>  

만약 두가지 조건을 적용하고 싶다면 다음과 같이 할 수 있다.  
```bash
db.zips.find({"state" : "NY", "city" : "ALBANY"})
```

조건 없이 모든 데이터를 조회할 때에는 `find`에 인자를 넣지 않고 조회한다.
```bash
db.zips.find()
```

#### pretty()
```bash
db.zips.find().pretty()
```
`pretty()` 는 도큐먼트의 구조와 각각의 필드, 값의 쌍을 조금 더 읽기 편하게 만들어준다.  

#### count()
```bash
db.zips.find().count()
```
데이터의 수를 조회하기 위해서 `count()`를 사용한다.  
`zips`안의 컬렉션 안 모든 데이터의 수가 출력된다.  

#### findOne()
조건 쿼리문을 작성하지 않은 상태로 `findOne()`을 사용하면 무작위 데이터 1개만 가져올 수 있다.  
```bash
db.zips.findOne()
```

## CREATE
각 도큐먼트의 고유의 값인 `_id`와 새로운 도큐먼트를 추가하는 방법에 대해 알아본다.  
모든 `MongoDB` 도큐먼트는 `_id` 필드를 기본 값으로 반드시 가져야 한다.  
`_id` 필드의 값은 각 도큐먼트를 구별하는 역할을 한다.  
<br>  

도큐먼트 내부의 필드와 값이 똑같다 할지라도, `_id`의 값이 다르면 서로 다른 도큐먼트로 간주한다.  
반면, 도큐먼트 내 필드와 값이 다르더라도, `_id` 값이 같으면 같은 도큐먼트로 여거 에러가 발생한다.  

<br>  

따라서 도큐먼트는 고유한 `_id`값을 가져야 한다.  
새로운 도큐먼트를 추가할 때, `_id`값에 임의로 고유한 값을 생성하여 사용할 수도 있지만,  
보통은 `ObjectId` 타입 (12byte, 24char)d의 값으로 사용한다.  
도큐먼트를 추가할 때 `_id` 필드와 값을 특정하지 않았다면,  
자동적으로 `_id` 필드가 생성되고 값에 `ObejctId` 타입이 할당된다.  

### insert
하나의 도큐먼트를 삽입할 때에는 다음과 같이 한다.  
```bash
db.zips.insert({
    "city" : "ALPINE",
    "zip" : "35014",
    "loc" : {
        "y" : 33.33165,
        "x" : 86.208934
    },
    "pop" 3062,
    "state" : "AL"
})
```

한 번에 다수의 도큐먼트를 삽입하기 위해서는 배열 안에 해당하는 도큐먼트를 담아줘야 한다.  
```bash
db.inspections.insert([{"test" : "1"}, {"test" : "2"}, {"test" : "3"}])
```
MongoDB가 업데이트되어, `insertOne`이나 `insertMany`를 사용하라고도 한다.

#### nInserted
`insert`를 수행하고 나면 출력값으로 `nInserted` 항목이 나온다.  
이 항목은 삽입된 도큐먼트의 수를 의미한다.  
만약 이 부분이 0이라면, 삽입된 도큐먼트가 없다는 뜻이므로, 도큐먼트 추가에 실패했음을 의미한다.  

#### ordered
다량의 도큐먼트가 삽입될 때, 작업을 수행하기 위한 기본 프로세스가 배열 안의 리스트 된 순서대로 진행된다.  
만약 중간에 에러가 발생할 경우, 그 이후는 실행되지 않는다.  
그러나 `insert` 명령어의 2번째 인자에 순서 옵션인 `ordered`를 추가하면 순서를 바꿀 수 있다.  
```bash
db.inspections.insert([{"test" : "1"}, {"test" : "2"}, {"test" : "3"}], {"ordred" : false })
```

#### 존재하지 않는 컬렉션에 insert
`MongoDB`는 사용자가 쉽게 새로운 컬렉션이나 데이터베이스를 생성하기를 원한다.  
만약 사용자가 존재하지 ㅇ낳는 컬렉션에 도큐먼트를 넣는 경우, 그와 동시에 컬렉션이 만들어진다.  

## UPDATE
mongo shell에서 도큐먼트를 업데이트하기 위한 방법에는 `updateOne`, `updateMany` 2가지 방법이 있다.  
`updateOne`은 `findOne`과 비슷하게,  
주어진 기준에 맞는 다수의 도큐먼트가 있다면, 그 중 기준에 맞는 첫 번째 도큐먼트 하나만 업데이트가 된다.  
반면 `updateMany`는 쿼리문과 일치하는 모든 도큐먼트를 업데이트한다.  

### updateMany
```bash
dp.zips.updateMany({"city" : "ALPINE"}, {"$inc" : {"pop" : 10, "<field1>" : "<increment value1>" , "<field2>" : "<increment value2>"}})
```
`updateMany`는 두가지를 인자로 받으며,  
첫번째 인자는 **업데이트 할 도큐먼트를 결정하는 조건**이며,  
두번쨰 인자는 **업데이트의 내용**이다.  

#### $inc
`$inc` 연산자는 `MQL`(MongoDB Query Language)의 업데이트 연산자로,  
업데이트 하려는 필드와 증가하는 값을 위와 같이 작성하여 다양한 필드의 값을 동시에 업데이트할 수 있다.  
즉, 예시에서 보이는 코드는 pop 필드를 10만큼씩 증가시키는 쿼리문이다.  

### updateOne
`updateOne` 또한 `updateMany`와 동일하게 파라미터를 받아동작한다.  

#### $set
`$set` 연산자는 주어진 필드에 지정된 값을 업데이트한다.  
```bash
db.zips.updateOne({"zip" : "12345"}, {"$set" : {pop : 6235}})
```

#### $push
`$push` 연산자는 배열로 이루어진 필드의 값에 요소를 추가하기 위해 쓴다.  
```bash
db.grades.updateOne({"student_id" : 250, "class_id" : 339}. {"$push" :{"scores" : {"type" : "extra credit", "score" : 100}}})
```

## DELETE
mongo shell을 사용하여 도큐먼트 및 컬렉션을 삭제할 때, `deleteOne()`과 `deleteMany()`를 사용할 수 있다.  
앞서 배웠던 `updateOne()`, `updateMany()`와 작동 방식이 비슷하다.  
<br>  

`deleteOne()`은 주어진 기준에 맞는 다수의 도큐먼트 중 첫 번째 도큐먼트 하나를 삭제한다.  
검색 쿼리문의 조건에 맞는 다수의 도큐먼트가 있다면, 의도하지 않은 도큐먼트가 삭제될 수 있다.  
그렇기 때문에 `deleteOne()`을 사용하는 경우, `_id`값으로 쿼리해 온 도큐먼트를 삭제하는 것이 좋다.  
기준을 충족하는 도큐먼트가 많을 경우에는 `deleteMany()`를 사용하여 다수의 도큐먼트를 삭제한다.  

### deleteOne
```bash
db.inspections.deleteOne({"id" : "fordeleting"})
```

### drop()
컬렉션을 삭제하기 위해서는 `drop()`명령어를 사용한다.  
```bash
db.inspection.drop()
```

## Reference
[MongoDB Documentation](https://www.mongodb.com/docs/manual/reference/operator/query/)