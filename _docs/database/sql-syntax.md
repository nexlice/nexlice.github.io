---
title: SQL Syntax
tags: 
 - SQL


description: Learn about the SQL Syntax!
---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->

# SQL
`SQL`은 Structured Qeury Language의 이니셜이다.  
`SQL`은 데이터베이스용 프로그래밍 언어이며, 데이터베이스에 query를 보내 원하는 데이터만을 뽑아올 수 있다.  
주로 `MySQL`, `Oracle`, `SQLite`, `PostgreSQL` 등, 다양한 관계형 데이터베이스에서 사용한다.  
SQL을 사용하기 위해서는 데이터의 구조가 고정되어 있어야 한다.  
<br>

이떄 Query란, `질의문`을 의미하며, 검색창에 적는 검색어 또한 Query의 일종이다.  
Query는 저장되어있는 정보를 필터하기 위한 질문이다.  

---  

## Achievement Goal
- SQL이 어떻게 이루어져 있는지 이해한다.  
- SQL 기본 query문을 사용할 줄 안다.  
- Schema의 설계 방법과 나은 방향성을 고안한다.  
- 서버와 클라이언트 사이에서 주고 받는 데이터를 database에 저장하여 영속성있게 저장할 수 있다. 

---  


## Database Syntax
### CREATE
```sql
# 데이터베이스 생성  
CREATE DATABASE 데이터베이스_이름;
```

---  

### USE
데이터베이스를 이용해 테이블을 만들거나, 수정, 삭제 등의 작업을 하려면,  
먼저 데이터베이스를 사용하겠따는 명령을 전달해야 한다.  
```sql
# 데이터베이스 사용
USE 데이터베이스_이름
```

---  

### CREATE TABLE
`USE`를 이용해 데이터베이스를 선택했다면, 이제 테이블을 만들 수 있다.  
```sql
# 테이블 생성
CREATE TABLE user (
    id int PRIMARY KEY AUTO_ICREMENT, # Primary key이면서 자동 증가됨.
    name varchar(255),
    email varchar(255)
)
```

---  

### INSERT INTO VALUES
```sql
INSERT INTO Customers (
    CustomerName, 
    Address, 
    City, 
    PostalCode,
    Country)
VALUES (
    'Hekkan Burger',
    'Gateveien 15',
    'Sandnes',
    '4306',
    'Norway');
```

---  

### DROP TABLE
테이블을 지울 때 `DROP`을 사용한다.  
```sql
DROP TABLE Persons;
```

---  

### TRUNCATE TABLE
테이블 내에 모든 데이터를 지울 떄 `TRUNCATE`를 사용한다.
```sql
TRUNCATE TABLE Persons;
```

---  

### ALTER TABLE
테이블에 새로운 속성을 추가하거나 삭제할 때 `ALTER`를 사용한다.
```sql
ALTER TABLE Persons
ADD Birthday DATE;

ALTER TABLE Persons
DROP COLUMN Birthday;
```

---  

### SHOW
```sql
# 현재 데이터베이스에 있는 모든 테이블 정보를 표시한다.
SHOW TABLES;
```

---  

### DESCRIBE
```sql
# 테이블 정보 확인
DESCRIBE user;
```

---  

### SELECT 
`SELECT`문에는 다양한 옵션을 넣어서 실행할 수 있다.  
SQL은 정해진 순서대로 컴파일을 하기 때문에, `SELECT`문의 실행 순서를 알아둬야한다.  
실행 순서는 다음과 같다.  

- FROM
- WHERE
- GROUP BY
- HAVING
- SELECT
- ORDER BY

에시로 다음을 보자.
```sql
SELECT CustomerId, AVG(Total)
FROM invoices
WHERE CustomerId >- 10
GROUP BY CustomerId
HAVING SUM(Total) >= 30
ORDER BY 2
```

위 쿼리문의 실행 순서는 다음과 같다.  
1. `FROM invoices` : invoices 테이블에 접근한다.
2. `WHERE Customer Id >= 10` : CustomerId 필드가 10 이상인 레코드들을 조회한다.  
3. `GROUP BY CustomerId` : CustomerId를 기준으로 그룹화 한다.  
4. `HAVING SUM(Total) >= 10` : Total 필드의 총합이 30 이상인 결과들만 필터링 한다.  
5. `SELECT CustomerId, AVG(Total)` : 조회된 결과에서 CustomerId 필드와 Total 필드의 평균값을 구한다.  
6. `ORDER BY 2` : `AVG(Total)` 필드를 기준으로 오름차순 정렬한 결과를 리턴한다.  

---  

SQL 문법은 비슷하고도 다른게 정말 많다.  
보통 한 문법에 종속된 문법이 많은데, 이 문서에서는 그들을 구별하기 위해서 명령어를 같이 작성한다.  

### SELECT FROM
```sql
SELECT 특성_1, 특성_2 
FROM 테이블_이름;

SELECT *
FROM 테이블_이름
```
> *는 와일드카드 (wildcard)로  전부 선택할 때에 사용한다.  

---  


### SELECT FROM WHERE AND
필터 역할을 하는 쿼리문이다. `WHERE`는 선택적으로 사용 가능하다.  
```sql
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 = "특정 값"

# 특정 값을 제외한 값 찾기 : <>
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 <> "특정 값"

# 특정 값을 제외한 값 찾기 : NOT
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE NOT 특성_1 = "특정 값"

# 특정 범위의 값을 포함하는 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 <= "특정 값"
```


---  


### SELECT FROM WHERE AND
조건을 동시에 만족해야 할 떄 `AND`를 사용한다.  
```sql
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 <= "특정 값_1"
AND 특성_2 = "특정 값_2"
```


---  


### SELECT FROM WHERE OR
조건을 적어도 하나 만족해야 할 떄 `OR`를 사용한다.  
```sql
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 <= "특정 값_1"
OR 특성_2 = "특정 값_2"
```


---  


### SELECT FROM WHERE LIKE
```sql
# 문자열에서 특정 값이 포함된 값들을 필터링 하기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 LIKE "%특정 문자열%"

# 문자열에서 특정 값으로 시작하는 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 LIKE "특정 문자열%"

# 문자열에서 특정 값으로 끝나는 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 LIKE "%특정 문자열"

# 문자열에서 특정 값으로 시작하고 끝나는 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 LIKE "특정 문자열_1%특정 문자열_2"

# 문자열에서 특정 값으로 시작하지 않는 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 NOT LIKE "특정 문자열%"

# 문자열에서 두번째 글자가 a인 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 LIKE "_a%"

# 문자열에서 첫번째 글자가 a,c,s인 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 LIKE "[acs]%"

# 문자열에서 첫번째 글자가 a,c,s가 아닌 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 LIKE "[!acs]%"

# 문자열에서 첫번째 글자가 a부터 f까지 아무 값인 값 찾기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 LIKE "[a-f]%"
```


---  


### SELECT FROM WHERE IN
```sql
# 리스트의 값들과 일치하는 데이터를 필터하기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 IN ("특정값_1", "특정값_2")

# 리스트의 값들과 일치하지 않는 데이터를 필터하기
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 NOT IN ("특정값_1", "특정값_2")
```


---  


### SELECT FROM WHERE IS
```sql
# 값이 없는 경우 NULL을 찾을 떄
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 IS NULL

# 값이 없는 경우를 제외할 때
# 값이 없는 경우 NULL을 찾을 떄
SELECT 특성_1, 특성2
FROM 테이블_이름
WHERE 특성_1 IS NOT NULL
```


---  


### SELECT FROM WHERE BETWEEN AND
```sql
# 특정 값 사이의 레코드를 찾을 때
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;

# 특정 값 사이가 아닌 레코드를 찾을 때
SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;

# 알파벳 정렬의 특정 구간을 찾을 떄
SELECT * FROM Products
WHERE ProductName BETWEEN 'Geitost' AND 'Pavlova';
```

---  

### GROUP BY
분류 별로 결과를 출력하고 싶을 때, `GROUP BY`를 사용한다.  
```sql
SELECT COUNT(CustomerID),
Country
FROM Customers
GROUP BY Country;
```

---  

### HAVING
`GROUP BY`로 조회된 결과를 필터링할 떄 사용한다.  
```sql
SELECT CustomerId, AVG(Total)
FROM invoices
GROUP BY CustomerId
HAVING AVG(Total) > 6.00
```

---  

### SELECT FROM ORDER BY
돌려받는 데이터 결과를 어떤 기준으로 정렬하여 출력할지 결정한다.  
`ORDER BY`는 선택적으로 사용할 수 있다.  
```sql
# 기본 정렬은 오름차순
SELECT *
FROM 테이블_이름
ORDER BY 특성_1

# 내림차순
SELECT *
FROM 테이블_이름
ORDER BY 특성_1 DESC

# 특성_1로 정렬 후, 특성_2로 정렬
SELECT *
FROM 테이블_이름
ORDER BY 특성_1, 특성_2
```
### SELECT FROM LIMIT
결과로 출력할 데이터의 개수를 정한다.  
`LIMIT`은 선택적으로 사용할 수 있다.  
쿼리문에서 사용할 떄에는 가장 마지막에 추가한다.  
```sql
SELECT *
FROM 테이블_이름
LIMIT 200
```


---  

### SELECT DISTINCT FROM
유니크한 값을 받고 싶을 떄에 사용한다.
```sql
SELECT DISTINCT 특성_1
FROM 테이블_이름
```


---  

### SELECT FROM JOIN ON
INNER JOIN(교집합)을 구현한다.  
조인하는 테이블의 ON절의 조건이 일치하는 겨로가만 출력한다.  
JOIN 대신에 INNER JOIN으로도 구현할 수 있다.  
```sql
SELECT *
FROM 테이블_1
JOIN 테이블_2 ON 테이블_1.특성_A = 테이블2.특성_B
```

---  

### SELECT FROM LEFT OUTER JOIN ON
OUTER JOIN(차집합)을 구현한다.  
조인하는 테이블의 ON절의 조건 중, 한쪽의 데이터를 모두 가져온다.  
`LEFT OUTER JOIN`, `RIGHT OUTER JOIN`, `FULL OUTER JOIN`으로 구현 가능하다.  
```sql
# LEFT OUTER JOIN으로 LEFT INCLUSIVE를 실행한다.
SELECT *
FROM 테이블_1
LEFT OUTER JOIN 테이블_2 ON 테이블_1.특성_A = 테이블_2.특성_B

# RIGHT OUTER JOIN으로 RIGHT INCLUSIVE를 실행한다.
SELECT *
FROM 테이블_1
RIGHT OUTER JOIN 테이블_2 ON 테이블_1.특성_A = 테이블_2.특성_B
```


---  


### SELECT FROM AS
테이블 속성 명에 별명을 붙일 때 사용한다.  
```sql
# 하나의 속성에 대해 별명 정하기
SELECT *
FROM Customers AS Consumers;

# 여러개의 속성을 사용하여도 별명을 각각 정할 수 있다.
SELECT CustomerName, Address, PosttalCode AS Pno
FROM Customers;
```


---  


### SELECT MIN FROM
파라미터로 테이블의 Column을 넣어준다.  
해당 속성이 가진 값들 중 최솟값을 가진 레코드를 보여준다.  
```sql
SELECT MIN(Price) 
FROM Products;
```

### SELECT MAX FROM
파라미터로 테이블의 Column을 넣어준다.  
해당 속성이 가진 값들 중 최댓값을 가진 레코드를 보여준다.  
```sql
SELECT MAX(Price) 
FROM Products;
```


---  


### SELECT AVG FROM
파라미터로 테이블의 Column을 넣어준다.  
해당 속성이 가진 값들의 평균을 보여준다.
```sql
SELECT AVG(Price) 
FROM Products;
```


---  


### SELECT SUM FROM
파라미터로 테이블의 Column을 넣어준다.  
해당 속성이 가진 값들의 총합을 보여준다.
```sql
SELECT SUM(Price) 
FROM Products;
```

---  


### SELECT COUNT FROM WHERE
조건을 만족하는 레코드의 개수를 반환한다.
```sql
SELECT COUNT(*)
FROM Products
WHERE Price = 18;
```


---  


### UPDATE SET
```sql
# 테이블의 column 값을 모두 바꾸고 싶을 떄
UPDATE Customers
SET City = 'Olso';
```


---  


### UPDATE SET WHERE
```sql
# 테이블의 column 값 중, 조건을 만족하는 튜플을 모두 바꾸고 싶을 떄
UPDATE Customers
SET City = 'Olso'
WHERE Country = 'Norway';
```


---  


### UPDATE SET , WHERE
두가지 이상을 SET으로 수정하고 싶다면 `,` 으로 연결한다.  
```sql
UPDATE Customers
SET City = 'Olso',
Country = 'Norway'
WHERE CustomerID = 32;
```

---  

### DELETE FROM
테이블로부터 모든 레코드를 지울 때 사용한다.  
```sql
DELETE FROM Customers;
```

---  

### DELETE FROM WHERE
조건을 만족하는 레코드만 지운다.  
```sql
DELETE From Customers
Where Country = 'Norway';
```

---  

### now()
현재 시간을 가져온다. `timestamp` 자료형에 쓸 수 있다.  
```sql
SELECT now();
```