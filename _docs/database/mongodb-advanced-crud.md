---
title: MongoDB Advanced CRUD
tags: 
 - $eq
 - $ne
 - $gt
 - $lt
 - $gte
 - $lte

description: Learn about the advanced MongoDB CRUD!
---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

{% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %}

# MongoDB Advanced CRUD
`MongoDB`에서 더 다양한 옵션을 통해 CRUD를 사용해보자.  

---

## Comparison Operators
`mongo shell`에서 연산자는 다음과 같은 문법으로 사용하며, 연산자의 종류는 아래와 같다.  
```json
{<field> : {<operator : <value>}}
```

- `$eq` : Equal to
- `$ne` : Not Equal to
- `$gt` : Greater than
- `$lt` : Less than
- `$gte` : Greater than or Equal to
- `$lte` : Less than or Equal to

### MongoDB GUI
MongoDB GUI에서 쿼리할 때에는 mongo shell에서 질의하는 것과는 달리 필터만 넣어주면 된다.  
아래의 `Filter`는 70초동안 자전거를 빌린 사람 중에서, 구독자가 아닌 사람이 몇명인지 몇명인지 조회할 수 있다.  
```json
{"tripduration" : {"site" : 70}, "usertype" : {"$ne" : "Subscriber"}}
```

### mongo shell
mongo shell에서의 쿼리는 `find`를 활용하여 결과를 받는다.  
경우에 따라 `pretty()`를 추가하여 보기좋게 만들 수 있다.  
```bash
db.trips.find({"tripduration" : {"site" : 70}, "usertype" : {"$ne" : "Subscriber"}})
```

이처럼 비교 연산자를 사용하면 특정 범위 내에서 데이터를 찾을 수 있다.  
비교 연산자를 지정하지 않으면 기본 연산자로 `$eq`가 사용된다.  

## Logic Operators
MQL(MongoDB Query Language)에는 `$and`, `$or`, `$nor`, 그리고 `$not` 4 가지 논리 연산자가 있다.  
이 중, `$nor`는 `$and`, `$or`, `$not`의 조합으로, 모든 절과 일치하지 않는 도큐먼트를 반환한다.  
<br>  

`$and`, `$or`, `$nor`는 유사한 구문을 사용하며, 연산자가 작동할 절의 배열 앞에 위치한다.  
```json
{<operator> : [{statement1}, {statement2}, ... ]}
```
`$not` 은 뒤에 오는 조건을 부정하기 때문에 배열 구문이 필요하지 않다.  
```json
{$not : {statement}}
```

### MongoDB GUI
다음 예시는 `No Violation Issued"`, `"Violation Issued"`를 제거한 값을 보여준다.  
```json
{"$nor" : [{"result": "No Violation Issued"}, {"result" : "Violation Issued"}]}
```

### $and
`$and`는 연산자가 지정되지 않았을 떄, 기본 연산자로 사용된다.  
즉, 다음 두 구문은 동일한 의미를 가진다.  
```json
{ "sector" : "Mobile", "result" : "Warning"}
{"$and" : [{ "sector" : "Mobile"}, {"result" : "Warning"}]}
```
이처럼 `$and`는 참이어야 하는 여러 기준이 있는 경우, 기본적으로 쿼리에 함축된다.  
이러한 성질을 이용하면 효과적으로 쿼리를 작성할 수 있다.  
```json
{"$and" : [{"total_employee": { "$gt" : 25 }}, { "total _employee": { "$lt" : 100 }}]}
{ "total_employee": {"$gt" : 25 }, "total _employee": { "$lt" : 100 }}
{ "total _employee": { "$gt" : 25, "$lt" : 100 }}
```

#### 언제 명시적으로 포함해야하는가
일반적인 규칙으로 쿼리에 동일한 연산자를 두 번 이상 포함해야할 때 `$and`를 명시한다.  
A에서 출발하거나 도착하는 비행편과 B 또는 C 비행기의 수를 확인할 때에는 다음과 같이 작성 가능하다.  
```json
{ "$and" : [{ "$or" : [{"dst_airport" : "A"}, {"src_airport" : "A"}]},
    {"$or" : [{"airplane" : "B"}, {"airplane" : "C"}]}]}.count()
```

## Expressive Query Operator
표현 연산자 `$expr`는 다양성을 가지고 있으며, 하나 이상의 작업을 수행할 수 있다.  

- 쿼리 내에서 `$expr`를 사용하여 집계 표현식(Aggregation Expression) `{ $expr : {<expression>}}` 을 사용할 수 있다.  
- 변수와 조건문을 사용할 수 있다.
- 같은 도큐먼트 내의 필드들을 서로 비교할 수 있다.  

### $
Trips 컬렉션에서 엏마나 많은 사람들이 자전거를 대여한 곳에 다시 자전거를 반납하는지 알아본자고 하자.  
해당 도큐먼트에서 모든 station은 그와 관련된 name 필드와 id 필드가 존재한다.  
이 중 `start station id`와 `end station id` 필드를 통해 쿼리를 작성해보자.  
```json
{"$expr" : {"$eq" : ["$start station id", "$end station id"]}}
```
위 표현식에서 사용된 필드 이름 앞의 `$`은 필드 이름 자체가 아니라, **해당 필드의 값**을 향하고 있다.  
즉, `$`는 필드의 값을 참조한다.  
따라서 `$`을 사용하여 각각의 도큐먼트마다 달라지는 특정 필드의 값을 변수처럼 비교할 수 있다.  
이렇게 `$expr`를 사용하여 같은 곳에서 대여하고 반납한 모든 결과에 대해 가져올 수 있다.  

### Aggregation Expression
Trips 컬렉션에서 몇 명이 1200초 이상 자전거를 타고, 다시 시작 지점에 자전거를 반납했는지 알아보자.  
```json
{"$expr" : {
            "$and" : [
                    {"$gt" : ["$tripduration", 1200]},
                    {"$eq" : ["$end station id", "$start station id"]}
                    ]
        }
}
```
MQL에서 비교 연산자 구문은 먼저 필드를 작성하고 나중에 적용되는 비교 연산자를 작성한다.  
그러나 이 구문은 집계 표현식을 사용한다.  
집계 구문에서는 연산자를 먼저 작성하고, 다음으로 필드와 값을 작성한다.  
> 즉, 집계 표현식은 다음과 같이 사용할 수 있다.  
> `{"$expr" : {<operator> : {<field>, <value>}}}`

## Array Operators

### $push
- 배열의 마지막 위치에 엘리먼트를 넣는다.  
- 비어있는 필드인 경우, 값을 요소로 하는 배열 필드를 추가한다.  
- 필드가 배열이 아닌 경우, 명령이 동작하지 않는다.  

### Array query
아래 예시와 같이 문자열 필드를 쿼리하는 방법으로 배열 필드에 쿼리를 시도하면,   
```json
{"amenities" : "Shampoo"}
```
쿼리에서 amenities가 배열이라는 것을 지정하지 않더라도,  
결과로 받은 도큐먼트에는 샴푸가 배열 요소 중 포함되어 있다.  
```json
{"amenities" : ["Shampoo"]}
```
샴푸를 대괄호로 묶어 배열로 만들어 쿼리를 작성하면, MongoDB는 배열 필드의 값으로 샴푸만 담긴 배열을 찾는다.  
추가적인 연산자가 없을 때에는 지정한 쿼리와 정확히 일치하는 도큐먼트만 찾는다.  

#### $all
배열 필드를 쿼리할 때, 배열 요소의 순서는 중요하게 작용한다.  
즉, 모든 요소가 도큐먼트에 존재할지라도 순서가 맞지 않을 경우, 아무것도 반환되지 않을 수 있다.  
<br>  

`$all`을 사용하면, 배열 요소의 순서와 상관없이 지정된 요소가 포함된 모든 도큐먼트를 찾을 수 있다.  
```json
{"amenities" : {"$all" : ["Wifi", "Internet", "Kitchen"]}}
```

#### $size
배열의 길이에 따라 결과 커서를 제한하기 위해서 쿼리에 `$size`를 추가할 수 있다.  
아래 조건식은 정확히 20개의 amenities를 가지며, 지정한 요소가 모두 배열에 포함된 도큐먼트만 반환하도록 한다.  
```json
{"amenities" : {"$size" : 20, "$all" : ["Wifi", "Internet", "Kitchen"]}}
```
특정한 요소를 찾지 않는다면, `$size`만을 사용하여 배열 길이로만 쿼리할 수도 있다.  

## Projection
도큐먼트에 너무 많은 필드와 정보가 있을 때, 원하는 필드만 가져올 수 있도록 `find` 문에 `projection`을 사용한다.  
```bash
db.listingsAndReviews.find(
    {"amenities" : {"$size" : 20 ,
                    "$all" : ["Internet", "Wifi", "Kitchen", "Headting", ...]}},
                    {"price" : 1, "address" : 1}).pretty()
```
두번째 인자로 위와 같이 `projection`을 추가할 경우, price와 address 필드만 결과 커서에 포함된다.  
<br>

`projection`의 문법에 대해 자세히 알아보자.  
프로젝션을 사용할 때, 0과 1을 사용해 겨로가에서 표시하거나, 표시하지 않을 필드를 지정할 수 있다.  
- 1 : 지정한 필드와 `_id` 필드만 가져온다.  
- 0 : 지정한 필드를 제외한 모든 필드가 표시된다.  

**한 번의 프로젝션에서 0과 1을 혼합할 수 없다.**  
1과 0을 혼용할 수 있는 유일한 경우는, 디폴트로 포함되는 `_id`필드를 제외하도록 특별히 요청할 때이다.  
이와 같은 요청이 없다면, `_id`필드가 기본적으로 도큐먼트에 포함되기 때문이다.  
![projection syntax]()

#### elemMatch
배열 필드의 서브 도큐먼트에 있는 요소에 어떻게 접근하는지 알아보자.  
다음 쿼리는 모든 유형의 평가에서 85점 이상의 성적을 받았고, 431 수업을 수강하는 모든 학생을 찾는 쿼리이다.  
```bash
db.grades.find({"class_id":431}, {"scores" : {"$elemMatch" : {"score" : {"$gt" : 85}}}})
```
`find` 명령에서는 첫 번쨰 인자인 쿼리에 해당하는 도큐먼트를 찾은 뒤, Projection한다.  
`$elemMatch`는 지정한 배열 필드가 도큐먼트에 존재하고, 조건에 맞는 요소가 있는 경우에만 해당 필드를 결과에 포함시킨다.  
일부 도큐먼트의 경우, 431이라는 class_id를 가졌지만 `$elemMatch`의 조건이 충족되지 않을 때,  
score 필드를 겨로가에 포함하지 않고, 디폴트로 포함되는 `_id` 필드만 결과에 포함할 수 있다.  
<br>  

`$elemMatch`는 쿼리의 프로젝션뿐만 아니라, find 명령의 쿼리 부분에서도 사용할 수 있다.  
어떤 수업에서든 extra credit을 받은 모든학생을 찾아보자.  
```bash
db.grades.find({"scores" : {"$elemMatch" : {"type" : "extra credit"}}}).pretty()
```
scores 배열에 type이라는 필드를 가지고 있고, 그 필드의 값이 extra credit인 학생을 찾는 쿼리이다.  
`$elemMatch`를 쿼리 부분에서 사용하기 때문에,  
결과로 배열에 있는 도큐먼트 요소의 type 필드의 값이 extra credit인 도큐먼트를 찾는다.  
또한 쿼리에 프로젝션이 없기 때문에, 결과에 각 도큐먼트의 모든 필드가 포함된다.  

## Querying Subdocuments
`MongoDB`에서는 유연한 데이터 모델링을 통해 개발자가 데이터를 저장할 방법을 결정할 수 있다.  
그래서 `MongoDB`에서는 일반적으로 서브 도큐먼트 또는 배열로 저장한다.  
위에서 `$elemMatch`를 통해 배열 내의 필드를 쿼리하는 방법을 알아보았다.  
이제는 서브 도큐먼트를 쿼리하는 방법에 대해 알아보자.  

### Dot notation
도큐먼트의 필드에 접근하기 위해서 `.`을 사용한다.  
다음은 start station location 도큐먼트의 type필드가 Point인 도큐먼트를 하나 조회하는 쿼리이다.
```bash
db.trops.findOne({"start station location.type" : "Point"})
```
도큐먼트 안에 서브 도큐먼트가 또 존재한다면, `.`을 중첩 사용하여 접근이 가능하다.  


#### Array Index
배열 안의 특정 인덱스에 접근할 때에도 `.`를 사용한다.
![배열과 서브 도큐먼트 쿼리하기]()

### regex
요소에 특정 값이 포함되는 조건을 걸기 위해서 `$regex` 정규식 연산자를 사용한다.  
다음은 relationships 배열에서 이름이 Mark인 CEO가 몇 명인지 알아보는 쿼리이다.  
```bash
db.companies.find({"relationships.0.person.first_name" : "Mark", 
                    "realtionships.title" : { "$regex" : "CEO"}},
                    {"name" : 1}).pretty()
```

### elemMatch
배열의 첫 번째 요소만이 아닌, 배열 요소 전체를 검색할 때 `$elemMatch`를 활용할 수 있다.  
다음은 배열 안에 있는 각 도큐먼트에서 relationships 배열에서 회사를 떠난 사람 중, 이름이 Mark인 사람을 찾는 쿼리이다.  
```bash
db.companies.find({"relationships" : {"$elemMatch" : {
                                                        "is_past" : true,
                                                        "person.first_name" : "Mark"}}},
                    {"name" : 1}).pretty()
```

## Reference
[MongoDB Documentation](https://www.mongodb.com/docs/manual/reference/operator/query-array/)