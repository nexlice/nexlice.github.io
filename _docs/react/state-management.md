---
title: State Management
tags: 
 - react
 - state
 - state manager
 - props drilling
 - single source of truth

description: Learn about the concepts of State Management!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

{% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %}

## State management
`state`란, 변하는 데이터이다. 특히 FE 개발에서는 동적으로 표현되는 데이터이다.  
리액트에서 서로 다른 컴포넌트가 동일한 상태를 다룬다면, 이 출처는 오직 한 곳이어야 한다.  
만일 사본이 있을 경우, 두 데이터는 서로 동기화(sync)하는 과정이 필요하다.  
이 과정이 결코 쉽지 않기 때문에, 데이터 무결성을 위해, 동일한 데이터는 항상 같은 곳에서 가져오는 습관을 들여야 한다.  
`Single source of truth`(신뢰할 수 있는 단일 출처)원칙은 FE가 아니더라도 중요한 원칙이다.  

---

### Examples
**테마 변경**  
다크 모드와 같은 기능을 쓸 때 모든 페이지, 모든 컴포넌트에 적용이 되어야하기 때문에,  
테마 설정을 전역으로 관리할 수도 있다.  

**Globalization**  
사용자가 사용하는 브라우저나, 운영체제가 특정 언어를 사용하고 있음을 알아내서,  
UI에 필요한 텍스트 리소스를 저장한 후, 전역 상태로 관리하기도 한다.  
이 기능의 경우에도 모든 컴포넌트에서 사용자 언어로 표현이 되어야 하기 때문에, 전역에서 상태 관리가 필요하다.  

**Undo/Redo**  
화면에 표시되는 모든 내용을 저눕 상태 객체로 만들어 저장한다면,  
원하는 특정 상태를 바탕으로 컴포넌트를 표현할 수 있다.  

---

### 상태 라이브러리
- 전역 상태를 위한 저장소를 제공한다.  
- props drilling 문제를 해결한다.  

> props drilling이란,  
> 중간 자식이 해당 props가 필요하지 않아도 하위 자식에게 props를 전달해야하는 상황에서,  
> 중간 자식 컴포넌트에 props를 만들어 자식에게 넘기는 문제를 말한다.  
> 전역 상태 저장소가 있고, 해당 저장소에 접근시킴으로 문제를 해결한다.  

---

### 필요성
상태 관리 툴이 반드시 필요하지는 않다.  
Redux의 개발자인 Dan abamov도 'You Might Not Need Redux' 아티클을 통해,  
React 공식 문서의 "React로 사고하기"만 잘 따라가도 문제를 해결할 수 있다 언급한다.  
그러므로 장단점을 분명히 인지하고 상태 관리툴을 써야한다.  
무엇보다, 상태 관리의 기본기라고 할 수 있는, **상태가 어디에 위치해야하는지**를 먼저 익혀야 한다.  
