---
title: NoSQL
tags: 
 - NoSQL
 - Document
 - RDBMS
 - non RDBMS

description: Learn about the Concept of NoSQL!
---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->

# NoSQL
`NoSQL`은 `SQL`앞에 붙은 No에서 알 수 있듯이, 주로 데이터가 고정되어 있지 않은데이터 베이스를 가리킨다.  
이 문서에서는 `NoSQL`과 `SQL`의 차이를 알아보고, `NoSQL`의 개념에 대해 학습한다.  

---  

## SQL vs NoSQL
데이터베이스는 크게 **관계형 데이터베이스**와 **비관계형 데이터베이스**로 구분한다.  
관계형 데이터베이스는 **SQL**을 기반으로하고, 비관계형 데이터베이스는 **NoSQL**로 데이터를 다룬다.  
SQL과 NoSQL은 만들어진 방식, 저장하는 정보의 종류, 그리고 저장하는 방법 등에 차이가 있다.  

---  

## RDB
관계형 데이터베이스에서는 테이블의 구조와 데이터 타입 등을 사전에 정의하고,  
테이블에 정의된 내용에 알맞은 형태의 데이터만 삽입할 수 있다.  
<br>
관계형 데이터베이스는 행(row)과 열(column)로 구성된 테이블에 데이터를 저장한다.  
각 열은 하나의 속성에 대한 정보를 저장하고, 행에는 각 열의 데이터 형식에 맞는 데이터가 저장된다.  
<br>
특정한 형식을 지키기 때문에, 데이터를 정확히 입력했다면, 데이터를 사용할 때에는 매우 수월하다.  
관계형 데이터베이스에서는 스키마가 뚜렷하게 보인다.  
다시 말해, 관계형 데이터베이스에서는 테이블 간의 관계를 직관적으로 파악할 수 있다.  

> 대표적인 관계형 데이터베이스는 MySQL, ORacle, SQLite, PostgreSQL, MariaDB 등이 있다.  

---  

## NoSQL
`NoSQL`이 `SQL`과 반대되는 개념처럼 사용되지만, `NoSQL`에 스키마가 반드시 없는 것은 아니다.  
관계형 데이터베이스에서는 데이터를 입력할 떄 스키마에 맞게 입력해야 하지만,  
`NoSQL`에서는 데이터를 읽어올 때 스키마에 따라 데이터를 읽어온다.  
이런 방식을 `schema on read`라고도 한다.  
<br>

읽어올 때만 데이터 스키마가 사용된다고 하여, 데이터를 쓸 때 정해진 방식이 없는 것은 아니다.  
데이터를 입력하는 방식에 따라, 데이터를 읽어올 떄 영향을 미친다.  

> 대표적인 NoSQL 은 MongoDB, Casandra 등이 있다.
<br>

NoSQL 기반의 비관계형 데이터베이스는 보통 다음과 같이 구성된다.  
- Key-Value 타입 : 속성을 `Key-Value`의 쌍으로 나타내는 데이터를 배열의 형태로 저장한다.  
여기서 **Key**는 속성의 이름을 뜻하고, **Value**는 속성에 연결된 데이터 값을 의미한다.  
Redis, Dynamo 등이 대표적인 Key-Value 형식의 데이터베이스이다.  

- 문서형(Document) 데이터베이스 : 데이터를 테이블이 아닌 문서처럼 저장하는 데이터베이스를 의미한다.  
많은 문서형 데이터베이스에서 JSON과 유사한 형식의 데이터를 문서화하여 저장한다.  
각각의 문서는 하나의 속성에 대한 데이터를 가지고 있고, 컬렉션이라 하는 그룹으로 묶어서 관리한다.  
대표적인 문서형 데이터베이스에는 MongoDB가 있다.  

-  Wide-Column 데이터베이스 : 데이터베이스의 열(column)에 대한 데이터를 집중적으로 관리하는 데이터베이스이다.  
각 열에는 `Key-Value` 형식으로 데이터가 저장되고, `컬럼 패밀리`(column families)라고 하는 열의 집합체 단위로 데이터를 처리할 수 있다.  
하나의 행에 많은 열을 포함할 수 있어서 유연성이 높다.  
데이터 처리에 필요한 열을 유연하게 선택할 수 있다는 점에서 규모가 큰 데이터 분석에 주로 사용된다.  
대표적인 Wide-Column 데이터베이스에는 Cassandra, HBase가 있다.  

- 그래프(Graph) 데이터베이스 : 자료구조의 그래프와 비슷한 형식으로 데이터 간의 관계를 구성하는 데이터베이스이다.  
노드(nodes)에 속성별(enitities)로 데이터를 저장한다.  
각 노드간 관계는 선(edge)으로 표현한다.  
대표적인 그래프 데이터베이스에는 Neo4J, InfiniteGraph가 있다.  

---  

### RDBMS vs non RDBMS

||관계형 데이터베이스|비관계형 데이터베이스|
|:---:|:---|:---|
|데이터 저장 (Storage)|SQL을 이용하여 데이터를 테이블에 저장한다.<br>미리 작성된 스키마를 기반으로 정해진 형식에 맞게 데이터를 저장한다.|key-value, document, wide-column, graph 등의 방식으로 데이터를 저장한다.|
|스키마(Schema)|SQL을 사용하려면, 고정된 형식의 스키마가 필요하다.<br>따라서 처리하려는 데이터 속성별로 열(column)에 대한 정보를 미리 정해야한다.<br>그래서 정보를 요청할 때, SQL과 같이 구조화된 쿼리 언어를 사용한다.|비관계형 데이터베이스의 쿼리는 **데이터 그룹 자체**를 조회하는 것에 초점을 둔다.<br>그래서 구조화되지 않은 쿼리 언어로도 데이터 요청이 가능하다.<br>UnQL(Unstructured Query Language)라 말하기도 한다.|
|확장성(Scalability)|일반적으로 SQL기반의 관계형 데이터베이스는 수직적으로 확장한다.<br> 높은 메모리, CPU를 사용하는 확장이라고도 한다.<br>데이터베이스가 구축된 하드웨어의 성능을 많이 이용하기 때문에 비용이 많이 든다.<br>여러 서버에 걸쳐서 데이트베이스의 관계를 정의할 수 있지만, 매우 복잡하고 시간이 많이 소요된다.|NoSQL로 구성된 데이터베이스는 수평적으로 확장한다.<br>저렴한 범용 하드웨어나, 클라우드 기반의 인스턴스에 NoSQL 데이터베이스를 호스팅할 수 있기 때문에,<br>수직적 확장보다 상대적으로 비용이 저렴하다.

---  

## Which DB should you use
데이터베이스를 구축하는 방법을 선택하는 것에 대해 완벽한 솔루션은 없다.  
그렇기 때문에 많은 개발자는 유저의 요구를 충족시키기 위해,  
관계형, 비관계형 데이터베이스를 모두 사용하여 서비스에 맞게 설계하고 있다.  
<br>
NoSQL 기반의 비관계형 데이터베이스가 확장성이나 속도 면에서 더 뛰어나지만,  
고차원적으로 구조화된 SQL 기반의 데이터베이스가 더 좋은 성능을 보여주기도 한다.  
다음 사용 사례들을 살펴보자.  

---  

**Using RDBMS**  
- 데이터베이스의 ACID 성질을 준수해야하는 경우  
ACID는 데이터베이스에서 실행되는 하나의 트랜잭션에 의한 상태의 변화를 수행하는 과정에서,  
안정성을 보장하기 위해 필요한 성질들의 모음이다.  
SQL을 사용하면 데이터베이스가 상호작용하는 방식을 정확하게 규정할 수 있기 때문에,  
데이터베이스에서 데이터를 처리할 때 발생할 수 있는 예외적인 상황을 줄이고, 데이터베이스의 무결성을 보호할 수 있다.  
<br>
전자 상거래를 비롯한 **모듬 금융 서비스**를 위한 소프트웨어 개발에서는 반드시 데이터베이스의 ACID 성질을 준수해야 한다.  
그래서 잉런 경우에는 일반적으로 SQL을 이용한 관계형 데이터베이스를 사용한다.  

- 소프트웨어에 사용되는 데이터가 구조적이고 일관적인 경우  
프로젝트의 규모가 많은 서버를 필요로 하지 않고, 일관된 데이터를 사용하는 경우,  
관계형 데이터베이스를 사용하는 경우가 많다.  
다양한 데이터 유형과 높은 트래픽을 지원하도록 설계된 NoSQL 데이터베이스를 사용해야만 하는 이유가 없기 때문이다.  

---

**Using non-RDBMS**
- 데이터의 구조가 거의 또는 전혀 없는 대용량의 데이터를 저장하는 경우  
대부분의 NoSQL 데이터베이스는 저장할 수 있는 데이터의 유형에 제한이 없다.  
필요에 따라, 언제드닞 데이터의 새 유형을 추가할 수 있다.  
소프트웨어 개발에 정형화되지 않은 많은 양의 데이터가 필요한 경우, NoSQl을 적용하는 것이 효율적이다.  

- 클라우드 컴퓨팅 및 저장공간을 최대한 활용하는 경우  
클라우드 기반으로 데이터베이스 저장소를 구축하면, 저렴한 비용의 솔루션을 제공받을 수 있다.  
소프트웨어에 데이터베이스의 확장성이 중요하다면, 별다른 번거로움 없이 확장할 수 있는 NoSQL 데이터베이스를 사용하자.  

- 빠르게 서비스를 구축하는 과정에서 데이터 구조를 자주 업데이트하는 경우  
NoSQL 데이터베이스는 스키마를 미리 준비할 필요가 없기 때문에 빠르게 개발하는 과정에 매우 유리하다.  
시장에 빠르게 프로토타입을 출시해야 하는 경우가 이에 해당한다.  
<br>
또한 소프트웨어 버전별로 많은 다운타임(데이터베이스 서버를 오프라인으로 전환하여 데이터 처리를 진행하는 작업 시간) 없이,  
데이터 구조를 자주 없데이트 해야하는 경우, 스키마를 매번 수정해야하는 관계형 데이터베이스보다,  
NoSQL 기반의 비관계형 데이터베이스를 사용하는게 더 적합하다.  