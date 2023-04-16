---
title: Basic Jargons
tags: 
 - Schema
 - Entity
 - Table
 - Data
 - Field
 - Record
 - Key
 - Relation
 - Self-referencing

description: Learn about the basic jargons of database!
---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->

# Basic jargons
데이터베이스에서 자주 사용하는 용어에 대해 알아보자.  

---  

## Schema
스키마는 데이터베이스에서 데이터가 구성되는 방식과 서로 다른 엔티티 간의 관계에 대한 설명이다.  
즉, 데이터베이스의 청사진과 같다.  

---  

## Entity
고유한 정보의 단위이다.  
업무에 필요하고 유용한 정보를 저장하고 관리하기 위한 "어떤 것"이라고 할 수 있다.  
데이터베이스 내에서는 테이블을 지칭한다.  
<br>
엔티티는 유일한 식별자가 있어야 하며, 두 개 이상의 인스턴스의 집합이여 한다.  
또한 엔티티 간의 관계가 존재해야 한다. 

---  

## Table (Relation)
사전에 정의된 열의 데이터와 타입대로 작성된 데이터가 행으로 축적되는 곳이다.

---  

## Data
각 항목에 저장되는 값이다.

---  

## Field (Column)
엔티티에는 해당 엔티티의 특성을 설명하는 Field가 있다.  
테이블의 열에 해당한다.  

---  

## Record (Tuple)
테이블의 한 행에 저장된 데이터이다.  

---  

## Key
테이블의 각 레코드를 구분할 수 있는 값이다.  
레코드마다 고유한 값을 가지며, 기본키와 외래키 등이 있다.  

---  

## Relation
테이블과 테이블 사이의 관계를 나타내며, 다음 4가지로 나눌 수 있다.  

- 1:1
- 1:N
- N:N
- Self referencing

## Self referencing
User 테이블 안에 `user_id`와 `recommend_id`가 있다고 하자.  
한 명의 유저는 한 명의 추천인을 가질 수 있다.  
그러나 여러 명이 한 명의 유저를 추천인으로 등록할 수 있다.  
<br>  
1:N 관계와 유사하지만, 일반적으로 일대다 관계는 서로 다른 테이블의 관계를 나타낼 때 표현하는 방법이다.  