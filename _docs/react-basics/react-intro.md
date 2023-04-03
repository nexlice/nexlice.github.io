---
title: React Basics
tags: 
 - React
 - eclarative
 - Component
 - JSX
 - Bable

description: Learn about the concept of React!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->

# React Intro

---

## Achievement Goals
- `React`의 3가지 특징에 대해서 이해하고, 설명할 수 있다.
- `JSX`가 왜 명시적인지 이해하고, 바르게 작성할 수 있다.
- `React 컴포넌트` (`React Component`)의 필요성에 대해서 이해하고, 설명할 수 있다.
- `create-react-app`으로 간단한 개발용 `React`앱을 실행할 수 있다.

---

## What is React
프론트 엔드 개발을 위한 자바스크립트 오픈소스 라이브러리.  
리앤트는 선언형이고, 컴포넌트 기반이고, 다양한 곳에서 활용할 수 있다는 특징이 있다.  

### Declarative
선언형 프로그래밍이란, 개발자가 원하는 결과를 코딩하는 것을 의미한다.  
반면 명령형(Imperative)은 개발자가 처음부터 하나하나 원하는 작업을 코딩하는 것을 의마한다.  
리액트는 한 페이지를 보여주기 위해 `HTML`, `CSS`, `JavaScript`로 나눠 적기 보다는,  
하나의 파일에 명시적으로 작성할 수 있도록 `JSX`를 활용한 선언형 프로그래밍을 지향한다.  

선언형 언어이기 때문에, 개발자가 코드만 보고도 웹 서비스를 가늠할 수 있다.  
리액트는 하나의 기능 구현을 위해 여러 종류의 코드를 묶어둔 `컴포넌트`를 기반으로 개발한다.  
`컴포넌트`로 분리하면 서로 독립적이고 재사용 가능하기 때문에, 기능 자체에 집중하여 개발할 수 있다.  

### Versatility  
**Learn Onece, Write Anywhere**  
리액트는 자바스크립트 프로젝트 어디에든 유연하게 적용될 수 있다.  
`facebook`에서 관리되어 안정적이고, 가장 유명하며 `React Native`로 모바일 개발도 가능하다.  

---

## JSX
`JSX`는 `JavaScript XML`의 줄임말로 문자열도 아니고 `HTML`도 아니다.  
리액트에서 UI를 구성할 때 사용하는 문법으로 `JavaScript`를 확장한 문법이다.  
이 문법을 이용해 우리는 React 엘리먼트를 만들 수 있다.  

### Bable
`JSX`는 `JavaScript`가 확장된 문법이지만, 브라우저가 바로 실행할 수 있는 `JavaScript` 코드가 아니다.   
따라서 브라우저가 이해할 수 있는 `JavaScript` 코드로 변환을 해주어야 한다.  
이때 이용하는 것이 바로 `Babel`이다.  
`Babel`은 `JSX`를 브라우저가 이해할 수 있는 `JavaScript`로 컴파일한다.  
컴파일 후, `JavaScript`를 브라우저가 읽고 화면에 렌더링할 수 있다.  

### DOM vs React JSX
리액트에서는 `DOM`과 다르게 `CSS`, `JSX` 문법만을 가지고 웹 어플리케이션을 개발할 수 있다.  
즉, 컴포넌트 하나를 구현하기위해서 필요한 파일이 줄어들었고, 한 눈에 컴포넌트를 확인할 수 있게 되었다.  
`JSX`를 사용하면 `JavaScript`만으로 마크업 형태의 코드를 작성하여 `DOM`에 배치할 수 있게된다.  


### Why JSX?
`DOM`에서 자바스크립트와 함께 사용하기 위해서는 자바스크립트와 `HTML`을 연결하기 위한 작업이 필요했다.  
`Inline` 방식이나 `script` 태그를 이용하여 `JavaScript` 파일을 연결할 수도 있다.  
하지만 리액트에서는 `JSX`를 이용하여 `DOM` 코드보다 명시적으로 코드를 작성할 수 있다.  
자바스크립트 문법과 `HTMl` 문법을 동시에 이용해 기능과 구조를 한 눈에 확인할 수 있다.  
이렇게 구조와 동작에 대한 코드를 한 뭉치로 적은 코드셋을 컴포넌트라 한다.  

> 물론 JSX 없이도 React 요소를 만들 수 있다.  
> 하지만 코드가 복잡하고 가독성이 떨어진다.  

---

## JSX Syntax
- 하나의 엘리먼트 안에 모든 엘리먼트가 포함되어야 한다.
JSX에서 여러 엘리먼트를 작성하고자 하는 경우, 최상위에서 opening tag와 closing tag로 감싸주어야 한다.  

- 엘리먼트 클래스 사용시, className으로 표기
React에서 HTML class속성을 지정하려면 className으로 표기해야한다.  

- JavaScript 표현식 사용 시, 중괄호를 이용한다.
중괄호를 사용하지 않으면 일반 텍스트로 인식한다.  

- 사용자 정의 컴포넌트는 대문자로 시작 (PascalCase)
React 엘리먼트가 JSX로 작성되면 대문자로 시작해야한다.  
소문자로 시작하면 일반적인 HTML엘리먼트로 인식한다.  

```javascript
function Hello() {
    return <div>Hello!</div>;
}

function HelloWorld() {
    return <Hello />;
}
```
- 조건부 렌더링에는 삼항 연산자를 사용한다.
```javascript
<div>
{
    (1+1 === 2) ? (<p>정답</p>) : (<p>탈락</p>) 
}
</div>
```

- 여러개의 HTML엘리먼트를 표시할 때, map() 함수를 이용한다.
map 함수를 사용할 때에는 반드시 "key" JSX속성을 넣어아한다.
만약 "key" JSX 속성을 넣지 않으면, 리스트의 각 항목에 key를 넣어야한다는 경고가 표시된다.  
```javascript
function Blog(){
    const content = posts.map((post) =>
        <div key = {post.id}>
            <h3>{post.title}</h3>
            <p>{post.content}</p>
        </div>
    );
}
```

### map을 이용한 반복
만약 데이터가 몇개 없다면 모든 데이터를 코드에 작성해도 좋다.  
이러한 작업을 하드코딩 (hard coding)이라고 한다.  
```javascript
const posts = [
    { id : 1, title: "Hello World", content: "Welcome to learning React!"}, 
    { id : 2, title: "Installation", content: "You can install React via npm."}
];

function Blog() {
    return (
        <div>
            <div>
                <h3>{posts[0].title</h3>
                <p>{posts[0].content}</p>
            </div>
            <div>
                <h3>{posts[0].title</h3>
                <p>{posts[0].content}</p>
            </div>
        </div>
    );
}
```

하지만 데이터가 많아진다면 데이터가 추가될 때마다 코드를 변경해야만 한다.  
데이터가 변경될 떄마다 알아서 렌더링 할 수 있도록 map을 활용한다.  
map의 특성은 다음과 같다.  
- 배열의 각 요소를
- 특정 논리(함수)에 의해
- 다른 요소로 지정(map)한다.

위의 코드를 반복적으로 작성해야하는 부분만 골라서 배열의 요소로 넣으면, `React`가 이를 인지하고 모든 요소를 렌더링한다.  
```javascript
const posts = [
    { id : 1, title: "Hello World", content: "Welcome to learning React!"}, 
    { id : 2, title: "Installation", content: "You can install React via npm."}
];

function Blog() {
    const postToElement = (post) => (
        <div>
            <h3>{post.title}</h3>
            <p>{post.content}</p>
        </div>
    );

    const blogs = posts.map(postToElement);

    return <div className = "post-wrapper">{blogs}</div>;
}
```

> return 문 안에서 map 메서드를 사용해도 되는가?  

사용 가능하다. JSX를 사용하면 중괄호 안에 모든 표현식을 포함할 수 있기 때문에,  
map 메서드의 결과를 return 문 안에 인라인으로 처리할 수 있다.  
코드 가독성을 위해 변수로 추출할지, 아니면 인라인에 넣을지는 개발자가 판단해야 할 몫이다.  

---

### key 속성
React에서 map메서드 사용 시, key 속성을 넣지 않으면, 리스트의 각 항목에 key를 넣어야 한다는 경고가 표시된다.  
key 속성의 위치는 map 메서드 내부에 있는 엘리먼트, 즉 첫 엘리먼트에 넣어준다.

> key 속성 값이 반드시 id가 되어야 하는가? id가 존재하지 않는다면?  

key 속성값은 가능하면 데이터에서 제공하는 id를 할당해야한다.  
key 속성값은 id와 마찬가지로 변하지 않고, 예상 가능하며, 유일해야하기 떄문이다.  
정 고유한 id가 없는 경우에만 배열 인덱스를 넣어서 해결할 수 있다.  
배열 인덱스는 최후의 수단(as a last resort)으로만 사용한다.  
배열에 관한 자세한 내용은[여기](https://ko.reactjs.org/docs/lists-and-keys.html#keys)에서 확인하자.  

```javascript
const posts = [
    { id : 1, title: "Hello World", content: "Welcome to learning React!"}, 
    { id : 2, title: "Installation", content: "You can install React via npm."}
];

function Blog() {
    const blogs = posts.map((post) => (
        <div key = {post.id}>
            <h3>{post.title}</h3>
            <p>{post.content}</p>
        </div>
    ));

    return <div className = "post-wrapper">{blogs}</div>;
}
```

---

## Component-Based React

---


### 컴포넌트로 생각하기
컴포넌트란 하나의 기능 구현을 위한 여러 종류의 코드 묶음이며, UI를 구성하는 필수 요소이다.  
모든 리액트 애플리케이션은 최소 한 개의 컴포넌트를 갖고 있으며,  
이 컴포넌트는 애플리케이션 내부적으로는 근원(root)이 되는 역할을 한다.  
이 최상위 컴포넌트는 근원의 역할을 하므로 다른 자식 컴포넌트를 가질 수 있다.  
이 계층적 구조(hierachy)를 트리구조로 형상화 할 수 있다.  

---

### HTML + CSS + JS vs React Component
만약 리액트로 짜지 않았다면 컴포넌트 위치의 수정 사항이 생겼을 때, 개발자는 적어도 다음 3가지를 수행하여야한다.  
- HTML 로 구조를 우선 바꾼다.
- CSS를 수정한다
- 변경된 구조와 디자인에 맞춰 DOM로직을 수정한다.

반면 컴포넌트로 개발을 하였다면, 다음 하나만 수행하면 된다.
- 변경하려는 UI에 맞추어 컴포넌트의 위치만 수정한다.

---

### Create React App
Create React App은 리액트 SPA를 쉽고 빠르게 개발할 수 있도록 만들어진 툴 체인이다.  
리액트 말고도 여러 도구들이 웹앱을 배포할 떄 사용된다.  
그 모든 도구들이 작동하는 방법을 알면 좋겠지만 쉽지 않다.  
그래서 툴체인을 만들어서 개발을 좀 더 쉽게 하도록 한다.  

---

### Installation
- 먼저 리액트 프로젝트를 보관하고 싶은 디렉토리로 이동한다.  
```bash
npx create-react-app {원하는 프로젝트 이름}
```
실행을 하면 react, react-dom과 같은 패키지들이 설치된다.  
Happy hacking! 문구가 나오면 성공적으로 설치한 것이다.  

---

### Directory
node_modules 디렉토리 안에 모듈들이 위치해있고, json파일에 모듈에 대한 버전들이 명세되어있다.  
package.json에서 scripts의 start를 제일 많이 쓰게된다.  
`react scripts start` 와 `npm run start`는 똑같은 명령어이다.  

---

### index.js
`document.querySelector`와 비슷한 역할을 하는 `document.getElementById`를 통해 루트를 찾고,  
우리가 개발할 App을 호출하는 모습이다.  

---

### App.js
앞서 index.js에서 확인했듯 코드를 수정하면 바로 변경점이 보인다.  
저장과 동시에 변경점을 화면에서 확인할 수 있는 것을 hot reloading이라고 한다.  