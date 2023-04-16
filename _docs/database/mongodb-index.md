---
title: MongoDB Index
tags: 
 - Index
 - createIndex
 - Unique
 - Partial
 - TTL
 - getIndexes
 - dropIndex

description: Learn about the MongoDB Index!
---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

{% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %}

# Index
저장된 데이터의 크기가 커질수록, 쿼리의 결과를 얻기까지 기다리는 시간은 점점 늘어난다.  
쿼리의 속도가 느려지는 경우(slow query)를 해결하려는 방법 중 하나로, 인덱싱을 사용할 수 있다.  

## Entrance Settings
한 도서의 색인, index는 찾고자 하는 대상이 사전식으로 나열되어있고, 각 대상의 위치도 표현되어 있다.  
이 위치를 참조하면 책 전체를 살필 필요 없이, 해당 대상이 언급된 페이지로 바로 이동할 수 있다.  
데이터베이스의 인덱스도 이와 유사하다.  

## createIndex
인덱스를 생성하기 위해서 `createIndex()` 메서드를 사용한다.  
`createIndex`의 파리미터로 인덱스를 적용할 필드를 전달한다.  
이에 따른 값을 `1`로 지정하면 오름차순으로, `-1`로 하면 내림차순으로 정렬한다.  
이때 필드명을 1개로 지정하면 `단일 필드 인덱스`, 필드명이 2개 이상이면 `다중 인덱스`(compound index)이다.  
```bash
db.collection_name.createIndex({<필드명1>: 1, <필드명2>: -1})
```

인덱스는 이 외에도 `createIndex()`메서드의 두번쨰 파라미터로 **속성**을 추가할 수 있다.
```bash
db.collection_name.createIndex({<필드명1>: 1}, {<속성 property>: true})
```

### properties
인덱스에 적용할 수 있는 속성은 다음과 같이 나뉜다.  

#### Unique
유일한 속성으로 `_id`필드와 같이 컬렉션에 단 한 개의 값만 존재할 수 있는 속성이다.  
이 속성을 각 인덱스에 적용할 수 있다.  
다음은 `members`라는 컬렉션의 각 도큐먼트에 존재하는 `user_id` 필드의 인덱스를 중복값이 없는 유일한 필드로 생성한다.  
```bash
db.members.createIndex({"user_id": 1}, { unique : true})
```

#### Partial
부분적 속성으로, 도큐먼트의 조건을 정해 일부 도큐먼트에만 인덱스를 적용한다.  
이 속성을 사용하면, 필요한 부분에만 인덱스를 사용하여 효율적으로 쿼리를 할 수 있다.  
이를 위해 `partialFilterExpression` 옵션을 사용한다.  
아래 코드는 `restaurants`라는 컬렉션에 `cuisine`, `name`이라는 두 개의 필드를 사용하여 다중 인덱스를 생성한다.  
이 인덱스는 별점이 4점 이상인 도큐먼트에만 적용된다.  
```bash
db.restaurants.createIndex({"cuisine": 1, "name": 1}, { partialFilterExpression : { rating: {$gt:4}})
```

#### TTL(Time-To-Live)
이 속성은 Date 타입 혹은 Date 배열 타입의 필드에 적용할 수 있다.  
이 속성을 사용하면, 특정 시간이 지난 후, 도큐먼트를 컬렉션에서 삭제한다.  
아래 예시는 인덱스에 TTL 속성을 추가하고, 이에 따라 `lastModifiedDate`와 3600초 이상 차이가 나면, 도큐먼트를 컬렉션에서 제거한다.  
```bash
db.eventlog.createIndex({"lastModifiedDate": 1}, {expireAfterSeconds: 3600})
```

### getIndexes
생성된 인덱스를 조회할 때는 `getIndexes` 메서드를 사용한다.  
```bash
db.collection_name.getIndexes()
```
인덱스를 생성하지 않았을 때는 `_id`값만 인덱스로 생성되어 있다.  

### dropIndex
생성된 인덱스를 삭제할 때는 `dropIndex` 메서드를 사용한다.  
```bash
db.collection_name.dropIndex(name)

# or
db.collection_name.dropIndex({<field>: 1})
```
`getIndexes` 메서드로 해당 인덱스의 `name`을 알 수 있다.  
그 `name`필드를 파라미터로 넣어 삭제할 인덱스를 지정할 수 있다.  
또한 삭제하려는 인덱스의 필드와 지정했던 값을 파라미터로 전달하여 삭제 가능하다.
<br>  

모든 인덱스를 삭제하고 싶을 때는 다음과 같이 복수형의 메서드를 사용한다.  
```bash
db.collection_name.dropIndexes()
```

## Usage
`infantsInfo` 데이터베이스의 쿼리에 인덱스를 생성하는 에제이다.  
다음과 같이 각 도큐먼트에서 키 80cm인 영유아의 몸게 정보를 오름차순으로 받오는 쿼리가 있다고 하자.  
```bash
db.infantsInfo.find({"tall":80}).sort("weight": 1).pretty()
```
이 경우 다음과 같이 `tall`과 `weight`에 대한 다중 인덱스를 만들 수 있다.  
```bash
db.infantsInfo.createIndex({"tall":1, "weight": 1})
```
이렇게 두 필드에 대한 다중 인덱스가 생성되면, 이 인덱스를 기준으로 특수한 자료 구조가 생성된다.  
그리고 이 인덱스 값을 기준으로 조회하면, 더 이상 모든 데이터를 조회하지 않고,  
해당 자료구조만 조회하여 쿼리하는 작업을 수행할 수 있다.  

## Reference
[MongoDB Documentation](https://www.mongodb.com/docs/manual/core/index-unique/)
