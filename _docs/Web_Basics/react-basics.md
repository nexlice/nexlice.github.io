---
title: React Basics
tags: 
 - React
 - eclarative
 - Component
 - JSX
 - SPA
 - Bable
 - Router
 - Browse Router
 - State
 - Props
 - Events
 - Data Flow

description: Learn about basic React!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

{% include alert.html type="danger" title="이 문서는 아직 미완성 문서입니다." %}

# React Intro

## Achievement Goals
- `React`의 3가지 특징에 대해서 이해하고, 설명할 수 있다.
- `JSX`가 왜 명시적인지 이해하고, 바르게 작성할 수 있다.
- `React 컴포넌트` (`React Component`)의 필요성에 대해서 이해하고, 설명할 수 있다.
- `create-react-app`으로 간단한 개발용 `React`앱을 실행할 수 있다.

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

>> 여기부터 수정

### 범용성 Learn Onece, Write Anywhere
리액트는 자바스크립트 프로젝트 어디에든 유연하게 적용될 수 있다.
페북에서 관리되어 안정적이고, 가장 유명하며 리액트 네이티브로 모바일 개발도 가능하다.  

## JSX
JSX는 JavaScript XML의 줄임말로 문자열도 아니고 HTML도 아니다.  
리액트에서 UI를 구성할 때 사용하는 문법으로 JavaScript를 확장한 문법이다.  
이 문법을 이용해 우리는 React엘리먼트를 만들 수 있다.  

## Bable
JSX는 JavaScript가 확장된 문법이지만, 브라우저가 바로 실행할 수 있는 JavaScript 코드가 아니다.   
브라우저가 이해할 수 있는 JavaScript 코드로 변환을 해주어야 한다.  
이때 이용하는 것이 바로 “Babel”이다.  
Babel은 JSX를 브라우저가 이해할 수 있는 JavaScript로 컴파일한다.  
컴파일 후, JavaScript를 브라우저가 읽고 화면에 렌더링할 수 있다.  

## DOM, 그리고 React JSX
리액트에서는 DOM과 다르게 CSS, JSX 문법만을 가지고 웹 어플리케이션을 개발할 수 있다.  
즉, 컴포넌트 하나를 구현하기위해서 필요한 파일이 줄어들었고, 한 눈에 컴포넌트를 확인할 수 있게 되었다.  
JSX를 사용하면 JavaScript만으로 마크업 형태의 코드를 작성하여 DOM에 배치할 수 있게된다.  


## JSX를 써야하는 이유
DOM에서 자바스크립트와 함께 사용하기 위해서는 자바스크립트와 HTML을 연결하기 위한 작업이 필요했다.  
Inline방식이나 script태그를 이용하여 Javascript파일을 연결할 수도 있다.  
하지만 리액트에서는 JSX를 이용하여 DOM코드보다 명시적으로 코드를 작성할 수 있다.  
자바스크립트 문법과 HTMl문법을 동시에 이용해 기능과 구조를 한 눈에 확인할 수 있다.  
이렇게 구조와 동작에 대한 코드를 한 뭉치로 적은 코드셋을 컴포넌트라 한다.  

## JSX 없이 React사용 가능한가?
JSX 없이도 React 요소를 만들 수 있다. 하지만 코드가 복잡하고 가독성이 떨어진다.  

## JSX 문법
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

## map을 이용한 반복
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

위의 코드를 반복적으로 작성해야하는 부분만 골라서 배열의 요소로 넣으면, React가 이를 인지하고 모든 요소를 렌더링한다.  
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

- return 문 안에서 map 메서드를 사용해도 되는가?
사용 가능하다. JSX를 사용하면 중괄호 안에 모든 표현식을 퐇마할 수 있기 때문에,  
map 메서드의 결과를 return 문 안에 인라인으로 처리할 수 있다.  
코드 가독성을 위해 변수로 추출할지, 아니면 인라인에 넣을지는 개발자가 판단해야 할 몫이다.  

## key 속성
React에서 map메서드 사용 시, key 속성을 넣지 않으면, 리스트의 각 항목에 key를 넣어야 한다는 경고기 표시된다.  
key 속성의 위치는 map 메서드 내부에 있는 엘리먼트, 즉 첫 엘리먼트에 넣어준다.

- key 속성 값이 반드시 id가 되어야 하는가? id가 존재하지 않는다면?
key 속성값은 가능하면 데이터에서 제공하는 id를 할당해야한다.  
key 속성값은 id와 마찬가지로 변하지 않고, 예상 가능하며, 유일해야하기 떄문이다.  
정 고유한 id가 없는 경우에만 배열 인덱스를 넣어서 해결할 수 있다.  
배열 인덱스는 최후의 수단(as a last resort)으로만 사용한다.  
https://ko.reactjs.org/docs/lists-and-keys.html#keys

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

## Component-Based
### 컴포넌트로 생각하기
컴포넌트란 하나의 기능 구현을 위한 여러 종류의 코드 묶음이며, UI를 구성하는 필수 요소이다.  
모든 리액트 애플리케이션은 최소 한 개의 컴포넌트를 갖고 있으며,  
이 컴포넌트는 애플리케이션 내부적으로는 근원(root)이 되는 역할을 한다.  
이 최상위 컴포넌트는 근원의 역할을 하므로 다른 자식 컴포넌트를 가질 수 있다.  
이 계층적 구조(hierachy)를 트리구조로 형상화 할 수 있다.  

### HTML + CSS + JS vs React Component
만약 리액트로 짜지 않았다면 컴포넌트 위치의 수정 사항이 생겼을 때, 개발자는 적어도 다음 3가지를 수행하여야한다.  
- HTML 로 구조를 우선 바꾼다.
- CSS를 수정한다
- 변경된 구조와 디자인에 맞춰 DOM로직을 수정한다.

반면 컴포넌트로 개발을 하였다면 다음 하나만 수행하면 된다.
- 변경하려는 UI에 맞추어 컴포넌트의 위치만 수정한다.

## Create React App
Create React App은 리액트 SPA를 쉽고 빠르게 개발할 수 있도록 만들어진 툴 체인이다.  
리액트 말고도 여러 도구들이 웹앱을 배포할 떄 사용된다.  
그 모든 도구들이 작동하는 방법을 알면 좋겠지만 쉽지 않다.  
그래서 툴체인을 만들어서 개발을 좀 더 쉽게 하도록 한다.  

### 설치
- 먼저 리액트 프로젝트를 보관하고 싶은 디렉토리로 이동한다.
```bash
npx create-react-app {원하는 프로젝트 이름}
```
실행을 하면 react, react-dom과 같은 패키지들이 설치된다.  
Happy hacking! 문구가 나오면 성공적으로 설치한 것~  

### 디렉토리
node_modules 디렉토리 안에 모듈들이 위치해있고, json파일에 모듈에 대한 버전들이 명세되어있다.  
package.json에서 sciprts의 start를 제일 많이 쓰게된다.  
react=scripts start 와 npm run start는 똑같은 명령어이다.  

### index.js
document.querySelector와 비슷한 역할을 하는 document.getElementById를 통해 루트를 찾고,  
우리가 개발할 App을 호출하는 모습이다.  

### App.js
앞서 index.js에서 확인했듯 코드를 수정하면 바로 변경점이 보인다.  
저장과 동시에 변경점을 화면에서 확인할 수 있는 것을 hot reloading이라고 한다.  

# React SPA
## Achievement Goals
- SPA (Single-Page Application) 개념을 이해하고 설명할 수 있다.
- SPA의 장, 단점에 대해 이해하고 설명할 수 있다.
- 와이어 프로엠을 보고 어느 부분을 컴포넌트로 구분해야 할 지 스스로 정할 수 있다.
- React에서 npm으로 React Router DOM을 설치 (npm install react-router-dom)하고 이용할 수 있다.
- React Router DOM을 이용하여 SPA를 구현할 수 있다.
- 라우팅 구조를 짤 수 있어야 하고, 이에 필요한 기초 문법들을 사용할 수 있어야 한다.

## SPA의 등장 배경
전통적인 웹사이트에서는 사용자가 웹사이트 내의 다른 페이지로 이동하면, 
브라우저가 페이지를 보여주기 위해 매번 HTML파일로 된 "페이지 전체"를 불러와야만 했다.  

### 전통적인 웹사이트의 한계와 단점
웹사이트가 보다 복잡해지고 애플리케이션의 형태를 가지게 되면서, 사용자와 서비스 사이에 더욱 많은 상호작용이 일어나게 되었다.  
하지만 이때마다 Header나 Navigation Bar 등과 같이 중복되는 요소들을 매번 불러오는 것이 깜빡이는 현상을 일으키며 서버와의 불필요한 트래픽을 발생시켰다.  ```SSR```
한편, 사용자 입장에서는 매번 모든 페이지를 불러옴에 따라 더 느린 반응성을 갖게 되었고, 이는 애플리케이션과 같은 사용자 경험을 제공하기 어렵게 만들었다.  

### SPA의 둥장
1990년대 후반에 HTML 문서 전체가 아닌, 업데이트에 필요한 데이터만 서버에서 전달받아 이 데이터를 JavaScript가 동적으로 HTML 요소를 생성해서 화면에 보여주는 방식이 개발되어 사용되기 시작하였다.  
2000년대 중반부터 이러한 개발 방식을 이용한 웹 애플리케이션이 보편화되었으며, 이것이 SPA이다.  

### SPA의 개념
SPA는 서버로부터 완전히 새로운 페이지를 불러오는 것이 아니라, 화면을 업데이트하기 위해 필요한 데이터만 서버에서 전달받아, 브라우저에서 해당하는 부분만 업데이트 하는 방식으로 작동하는 웹 애플리케이션이나 웹사이트를 말한다.  

### SPA의 장점
애플리케이션과 사용자 사이에 수시로 상호작용이 발생하는데, 이떄 페이지 전체를 렌더링하는 것이 아니라, 필요한 부분만 업데이트 하기 떄문에 SPA는 사용자의 행동에 빠르게 반응한다.  
서버 입장에서는 요청받은 데이터만 넘겨주면 되기 때문에 과거와 같은 과부하 문제도 현저히 줄일 수 있다.  
또한 화면 전체를 새로 렌더링할 필요가 없기 떄문에, 보다 나은 사용자 경험을 제공한다.  
이런 SPA 방식으로 만들어진 대표적인 서비스로는 Youtube가 있다. 이 밖에 facebook, airbnb, Netflix 등 우리가 일상적으로 사용하는 다양한 서비스들이 SPA 방식으로 제작되어 있다.  

### SPA의 단점
- 느린 첫 화면 로딩 시간
브라우저는 첫 화면 로딩 시에 HTML 파일을 읽어들인 후, 그 안의 script 요안에 있는 JavaScript 파일을 다시 받아오는 과정을 거친다.  
이때 첫 화면 로딩 시 읽어들인 HTML 파일은 거의 비어있고, 대부분의 코드는 JavaScript 파일 안에 들어있다 보니 자연스럽게 JavaScript 파일이 무거워진다.  
때문에 이 JavaScript 파일을 기다리는 시간으로 인해 첫 화면의 로딩 시간이 길어진다.  
- 검색 엔진 최적화
검색 엔진 최적화란 구글이나 네이버 같은 검색엔진이 자료를 수집하기 좋도록 웹 페이지를 구성하는 것을 뜻한다.  
여기서 검색 엔진의 작동 방식을 잠깐 알아보면, 검색 로봇이 웹 페이지에 있는 정보를 수집하고 분석해서, 그 결괏값에 인덱스를 만들어 보관하고 있다가, 사용자가 검색어를 입력하면, 보관하고 있던 인덱스에서, 검색어와 가장 연관성이 높은 웹 페이지들은 순서대로 보여주는 방식으로 작동한다.  
검색 로봇은 자료를 수집할 때에 웹 페이지의 URL은 물론이고 HTML 문서 내의 각종 태그나 링크 등을 분석한다. SPA는 HTML이 거의 비어있다 보니 검색 로봇이 충분한 자료를 수집하지 못한다.  
이 떄문에 검색 노출이 중요한 웹 애플리케이션은, 검색 엔진 최적화에 대한 대응책을 따로 마련해야 하고, 더불어 앱 안에서 브라우저의 앞으로 가기/뒤로 가기 등의 상태 관리도 해야하기 떄문에, 개발의 복잡도가 더욱 늘어난다.  
다만 SPA에서도 검색 엔진 최적화에 대응할 수 있도록 검색 엔진이 발전하고 있어서, 점차 이 단점은 사라지고 있는 추세이다.  


## Wireframe
React에서 컴포넌트를 어떻게 나누어야하는지, 그리고 컴포넌트를 나누는 것이 왜 중요한가?

### Wireframe과 Mockup
Wireframe은 디자인에 들어가기 전 단계로 선(wire)를 이용해 윤곽선(frame)을 잡는 것을 말한다. 이 작업을 통해 개발자는 디자인 컨셉과 사이트 기능에 대한 이해를 할 수 있다. 그리고 목업(Mockup)은 데스크탑, 스마트폰의 프레임을 덧씌워 직관적으로 이해하기 쉽게 디자인한 것을 말한다.  

### 웹 페이지 설계하기
페이지를 먼저 만들기보다는 어떤 컴포넌트를 만들고 이들을 조합할지부터 구상한다.  
다음은 유튜브 페이지를 만드는 예시이다.  
먼저 화면 상단의 경우, 상단 전체를 아우르는 Header라는 컴포넌트가 있고, 그의 자식으로 Search와 Setiing이라는 컴포넌트를 만들기로 하였다.  
Header 컴포넌트는 애플리케이션 내의 어떤 페이지에 가더라도 늘 상단에 위치하니, 이 부분을 감안해서 설계 로직을 작성한다.  
화면 중앙ㅇ데는 크리에이터들이 올린 영상을 담고 있는 ContentesList라는 컴포넌트가 있고, 그 안에는 동일한 형태를 가진 영상물들이 반복적인 형태로 화면을 구성하기 있기 때문에 Content라는 컴포넌트를 한 번만 만들어 재사용 한다.  
Content 컴포넌트는 영상과 관련된 데이터를 입력받아, UI에 맞게 화면에 출력해준다. 더불어 눈에 보이지는 않지만 클릭 시 해당 영상을 재상해주는 기능도 갖고 있다.  
컴포넌트가 UI의 필수 요소란 정의도 맞고, 각자 고유의 기능을 가지고 있다는 정의도 맞다.  
하지만 조금 더 고차원의 React 개발자라면, 애플리케이션 안에서 다뤄지는 데이터를 컴포넌트들끼리 보다 유기적으로 주고받을 수 있도록 설계해야 한다.  

## React Router
SPA는 하나의 페이지를 가지고 있지만 사실 한 종류의 화면만 사용하지 않는다.  
이를테면 Twilttler와 같은 SPA를 만들 떄, 메인 트윗 모음 페이지, 알림 페이지, 마이 트윗 페이지 등의 화면이 필요할 수 있다.  
또한 화면에 따라 "주소"도 달라진다.  
이렇게 다른 주소에 따라 다른 뷰를 보여주는 과정을 "경로에 따라 변경한다."라는 의미로 라우팅(Routing)이라고 한다.  
하지만 리엑트 자체에는 이 기능이 내장되어 있지 않다.  

### React Router
React SPA에서는 라우팅을 위해 React Router라는 라이브러리를 가장 많이 사용한다.  

#### React Router 주요 컴포넌트
- router
라우터 역할을 하는 BrowserRouter
- route matchers
경로를 매칭해주는 Routes와 Route
- route changers
경로를 변경하는 역할을 하는 Link  

이 컴포넌트들을 사용하기 위해서는 React Router 라이브러리에서 따로 불러와야한다.  
Import는 필요한 모듈을 불러오는 역할로 비구조화 할당(destructing assignment)과 비슷하게 이용할 수 있다.  
```javascript
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
```

#### 환경세팅
npm 명령어를 통해 간단하게 설치 가능하다.
```bash
npm install react-router-dom@^6.3.0
```

#### React Router Tutorial
```javascript
<BrowserRouter>
    <div>
        <nav>
            <ul>
                <li>
                    <Link to="/">Home</Link>
                </li>
                <li>
                    <Link to="/about">Mypage</Link>
                </li>
                <li>
                    <Link to="/dashboard">Dashboard</Link>
                </li>
            </ul>
        </nav>

        <Routes>
            <Route path="/" element = {<Home />} />
            <Route path="/about" element = {<Mypage />} />
            <Route path="/dashboard" element = {<Dashboard />} />
        </Routes>
    </div>
</BrowserRouter>
```
##### BrowseRouter
BrowseRouter는 웹 애플리케이션에서 HTML5의 API를 사용해 페이지를 새로고침하지 않고도 주소를 변경할 수 있는 역할을 해준다.  
아래와 같이 ReactDOM의 렌더 단계인 index.js에 넣어서 활용할 수도 있다. BrowseRouter가 상위에 작성되어 있어야 Route 컴포넌트를 사용할 수 있다.  

###### index.js
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowseRouter } from 'react-router-dom';

ReactDOM.render(<BrowserRouter><App/></BrowserRouter>, document.querySelector('#root'));
```

##### Routes, Route
경로를 매칭해주는 역할을 하는 컴포넌트이다.
- `<Routes>` 컴포넌트는 여러 ```<Route>``` 를 감싸서 그 중 경로가 일치하는 단 하나의 라우터만 렌더링을 시켜주는 역할을 한다. ```<Routes>``` 를 사용하지 않으면 매칭되는 모든 요소를 렌더링 한다.
- ```<Route>``` 컴포넌트는 path와 element 속성을 지정하여 해당 path에 어떤 컴포넌트를 보여줄지 정한다. 아래에서 나오는 Link 컴포넌트가 정해주는 URL 경로와 일치하는 경우에만 작동한다.

##### Link
경로를 연결해주는 역할을 하는 컴포넌트이다. 페이지 전환을 통해 페이지를 새로 불러오지 않고 애플리케이션을 그대로 유지하여 HTML5 History API를 이용해 페이지의 주소만 변경해준다.  
ReactDOM으로 렌더를 시키게되면 ```<Link>``` 컴포넌트는 ```<a>``` 태그로 바뀐다.
> React Router에서 ```<a>``` 태그가 아닌 ```<Link>``` 를 사용하는 이유는?  
> ```<a>``` 태그는 페이지를 전환하는 과정에서 페이지를 불러오기 때문에 다시 처음부터 렌더링을 시킨다. 즉, 새로고침 현상이 일어난다. 하지만 ```<link>``` 컴포넌트는 **페이지 전환을 방지하는 기능이 내장**되어있기 떄문에 SPA를 구현할 수 있다.

# React State & Props
## Achievement Goals
- State, Props의 개념에 대해서 이해하고, 실제 프로젝트에 바르게 적용할 수 있다.
- React 함수 컴포넌트(React Function Component)에서 State hook을 이용하여 State를 정의할 수 있다.
- React 컴포넌트 (React Component)에 props를 전달할 수 있따.
- 이벤트 핸들러 함수를 만들고 React에서 이용할 수 있따.
- 실제 웹 애플리케이션의 컴포넌트를 보고 어떤 데이터가 State이고 Props에 적합한지 판단할 수 있다.
- 실제 웹 애플리케이션 개발 시 State와 Props의 위치를 스스로 정할 수 있다.
- React의 단방향 데이터흐름 (One-way data flow)에 대해 자신의 언어로 설명할 수 있다.

## Props
- 컴포넌트의 속성(property)을 의미한다.  
이름, 성별과 같이 변하지 않는 외부로부터 전달받은 값으로, 웹 어플리케이션에서 해당 컴포넌트가 가진 속성에 해당한다.  

- 부모 컴포넌트(상위 컴포넌트)로부터 전달받은 값이다.  
React 컴포넌트는 javaScript 함수와 클래스로, props를 함수의 전달인다(arguments)처럼 전달 받아,  
이를 기반으로 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다.  
따라서, 컴포넌트가 최초 렌더링 될 때에 화면에 출력하고자하는 데이터를 담은, 초기값으로 사용할 수 있다.  

- 객체 형태이다.  
props로 어떤 타입의 값도 넣어 전달할 수 있도록 props는 객체의 형태를 가진다.  

- 읽기 전용이다.
props는 외부로부터 전달받아 변하지 않는 값이다.  
그래서 props는 함부로 변경될 수 없는 읽기 전용(read-only) 객체이다.  

> 읽기 전용 객체가 아니라면 props를 전달받은 하위 컴포넌트 내에서 porps를 직접 수정 시,  
props를 전달한 상위 컴포넌트으 ㅣ값에 영향을 미칠 수 있게 된다.  
즉, 개발자가 의도하지 않은 side effect가 생기게 되고,  
이는 React의 하향식 데이터 흐름 원칙에 위배한다.  

###  How to use props
props를 사용하는 방법은 아래 3단계로 이루어진다.  
1. 하위 컴포넌트에 전달하고자하는 값(data)과 속성을 정의한다.
2. props를 이용하여 정의된 값과 속성을 전달한다.  
3. 전달받은 props를 렌더링한다.

React에서 속성 및 값은 다음처럼 할당한다.  

```javascript
<Child attribute = { value } />
```


다음과 같은 상황이 있다고하자.  
``` javascript
function Parent() {
    return (
        <div className = "parent">
            <h1>I'm the parent</h1>
            <Child text = {"I'm child"}/>
        </div>
    );
};

function Child(props) {
    return (
        <div className = "child">
            <p>{props.text}</p>
        </div>
    );
};
```

Parent, Child 컴포넌트를 선언하고, Parent 컴포넌트가 Child 컴포넌트를 호출하는 구조이다.  
함수에 인자를 전달하듯이 React 컴포넌트에 props를 전달하고, 이 props가 필요한 모든 데이터를 갖고있다.  
  
props 렌더링은 JSX 안에 직접 불러서 사용하면 된다.  
다만 props는 객체이기 때문에, 이 객체의 {key : value} 는 Parent 컴포넌트에서 정의한 {attrivute : value} 의 형태를 띤다.  
따라서 JavaScript에서 객체의 value에 접근할 때 dot notation을 사용하는 것과 동일하게,  
props의 value 또한 dot notation으로 접근할 수 있다.  


``` javascript
function Parent() {
    return (
        <div className = "parent">
            <h1>I'm the parent</h1>
            <Child>"I'm child<Child/>
        </div>
    );
};

function Child(props) {
    return (
        <div className = "child">
            <p>{props.children}</p>
        </div>
    );
};
```
위처럼 값을 태그 사이의 value를 넣어 전달할 수 있다.  
이 경우, props.children를 이용하면 해당 value에 접근하여 사용가 능하다.  

```javascript
import "./styles.css";

const App = () => {
  const itemOne = "React를";
  const itemTwo = "배우고 있습니다.";

  return (
    <div className="App">
      <Learn text1={itemOne} text2={itemTwo} />
    </div>
  );
};

const Learn = (props) => {
  return (
    <div className="Learn">
      <p>
        {props.text1} {props.text2}
      </p>
    </div>
  );
};

export default App;
```
만약 여러개의 props를 전달하고 싶다면 whitespace로 구분하여 전달한다.  

## State assignment
Toggle Switch나,  Counter처럼 컴포넌트 내부에서 변할 수 있는 값이다.  
State로 사용할 수 있는 **상태**의 종류는 다음과 같다.  

- 나이, 현재 사는 곳, 취업 여부, 결혼/연애 여부, 토글, 체크박스 


아래는 State를 사용한 간단한 예시이다.
```javascript
import React, { useState } from "react";
import "./styles.css";

function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };
  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={handleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}

export default CheckboxExample;
```

### useState
React에서는 state를 다루는 바법 중 하나로 useState 함수를 제공한다.  
useState 자체는 state hook이라 부른다.  
체크박스로 예시를 들어 useState를 쓰는 과정은 다음과 같다.  

- React로부터 useState를 불러온다.
```javascript
import { useState } from 'react';
```

- 이후 useState를 컴포넌트 안에서 호출한다.  
useState를 호출한다는 것은 "state"라는 변수를 선언하는것과 같으며,  
이 변수의 이름은 아무 이름으로 지어도 된다.  
일반적인 함수는 함수가 끝날 때 사라지지만, state 변수는 React에 의해 함수가 끝나도 사라지지 않는다.  
```javascript
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

    // 위의 코드는 아래와 같다.
    const stateHookArray = useState(false);
    const isChecked = stateHookArray[0];
    const setIsChecked = stateHookArray[1];
}
```
구조적으로 isChecked, setIsChecked는 useState의 리턴값을 구조 분해 할당한 변수이다.  

- useState를 호출하면 배열을 반환하는데, 배열의 0번째 요소는 **현재 state**변수이고,  
1번째 요소는 **이 변수를 갱신할 수 있는 함수**이다.  
useState의 인자로 넘겨주는 값은 **state의 초기값**이다.  

```javascript
const [state 저장 변수, state 갱신 함수] = useState(상태 초기 값);
```

### update state
- state를 갱신하려면 state 변수를 갱신할 수 있는 함수인, ```setIsChecked```를 호출한다.  
- 위의 예시의 경우, ```input[type=checkbox]``` JSX 엘리먼트의 값 변경에 따라서 ```isChecked```가 변경되어야 한다.  
- ```input[type=checkbox]``` 엘리먼트의 값이 변경되면 ```onChange``` 이벤트가 발생한다.
- ```onChange``` 이벤트가 이벤트 핸들러 함수인 ```handleChecked```를 호출하고, 이 함수가 ```setIsChecked``` 를 호출한다.  
- ```setIsChecked```가 호출되면 호출된 결과에 따라 ```isChecked```변수가 갱신된다.  
- React는 새로운 ```isChecked``` 변수를 ```CheckboxExample``` 컴포넌트에 넘겨 해당 컴포넌트를 다시 렌더링 한다. 

```javascript
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };
  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={handleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}
```

### Precautions
- React 컴포넌트는 state가 변경되면 새롭게 호출되고, 리렌더링 된다.
- React state는 상태 변경 함수 호출로 변경해야한다. 즉, 강제로 변경을 시도하면 안된다.  
상태 변경 함수 사용은 React와 개발자의 약속이다.  
강제로 변경을 시도하면, 리렌더링이 되지 않는다거나, state가 제대로 변경되지 않는다.

```javascript
// 이러면 안된다!!!

function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const forceHandleChecked = (event) => {
    // setIsChecked(event.target.checked);
    isChecked = true;
  };
  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={forceHandleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}
```

## Event Handling
React의 이벤트 처리 (이벤트 핸들링; Event handling) 방식은 DOM의 이벤트 처리 방식과 유사하다.  
단, 몇 가지 문법 차이가 있다.  

- React에서 이벤트는 소문자 대신 카멜 케이스 (camelCase) 를 사용한다.
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 처리함수(이벤트 핸들러; Event handler)를 전달한다.  

HTML과  React의 이벤트 처리 방식차이는 아래와 같다.  
``` javascript
// HTML
<button onclick="handleEvent()">Event</button>

// React
<button onClick={handleEvent}>Event</button>
```

이벤트를 처리하는 데 여러 방식이 가능하다. 다음은 자주 사용되는 이벤트 처리에 대한 예시이다.
### onChange
```<input>``` ```<textarea>``` ```<select>```와 같은 폼(Form) 엘리먼트는 사용자의 입력값을 제어하는데 사용된다.  
React에서는 이러한 **변경될 수 있는 입력값**을 일반적으로 **컴포넌트의 state**로 관리하고 업데이트한다.  
```onChange```이벤트가 발생하면, ```e.target.value```를 통해 이벤트 객체에 담겨있는 ```input```값을 읽어올 수 있다.  
컴포넌트 return문 안의 ```input```태그에 ```value```와 ```onCHange```를 넣은 예시이다.  
```onChange```는 ```input```의 텍스타가 바뀔 때 마다 발생하는 이벤트이다.  
이벤트가 발생하면 ```handleChange```함수가 작동하며, 이벤트 객체에 담긴 ```input```값을 ```setState```를 통해 새로운 **state**로 갱신한다.

```javascript
function NameForm() {
    const [name, setName] = userState("");

    const handleChange = (e) => {
        setName(e.target.value);
    }

    return (
        <div>
            <input type = "text" value={name} onChange={handleChange}></input>
            <h1>{name}</h1>
        </div>
    );
};
```


### onClick
```onClick``` 이벤트는 사용자가 클릭이라는 행동을 하였을 때 발생하는 이벤트이다.  
버튼이나, ```<a>``` 태그를 통한 링크 이동 등과 같이 사용할 수 있다.  
위의 예시에서 ```onChange```에 버튼을 추가하여, 클릭시 ```input``` 태그에 입력한 이름이 alert를 통해 알림창이 팝업되도록 만들어보자.  

```javascript
// 잘못된 예시!

function NameForm() {
    const [name, setName] = userState("");

    const handleChange = (e) => {
        setName(e.target.value);
    }

    return (
        <div>
            <input type = "text" value={name} onChange={handleChange}></input>

            // 추가한 부분~
            <button onClick={alert(name)}>Button</button>

            <h1>{name}</h1>
        </div>
    );
};
```

위처럼 ```onClick```이벤트에 alert(name) 함수를 바로 호출하면 컴포넌트가 렌더링될 때 함수 자체가 아닌,  
함수 자체의 호출 결과가 ```onClick```에 적용된다.  
때문에 버튼을 클릭할 때가 아닌, 컴포넌트가 렌더링 될 때에 alert이 실행되고,  
따라서 그 결과인 undefined (함수는 리턴값이 없을 떄 undefined를 반환한다.)가 ```onClick```에 적용되어, 클릭했을 때 아무런 결과가 일어나지 않는다.  
따라서 ```onClick``` 이벤트에 함수를 전달 때는 함수를 호출하는 것이 아니라,  
아래와 같이 리턴문 안에서 함수를 정의하거나, 리턴문 외부에서 함수를 정의 후, 이벤트에 함수 자체를 전달해야한다.  
단, 두가지 방법 모두 arrow function을 사용하여 함수를 정의하여야, 해당 컴포넌트가 가진 state에 함수들이 접근할 수 있다.  

```javascript
function NameForm() {
    const [name, setName] = userState("");

    const handleChange = (e) => {
        setName(e.target.value);
    }

    const handleClick = () => {
        alert(name);
    };

    return (
        <div>
            <input type = "text" value={name} onChange={handleChange}></input>
            <button onClick={handleClick}>Button</button>
            <h1>{name}</h1>
        </div>
    );
};
```

### Practice - Select
```select tag```는 사용자가 drop down 목록을 열어 그 중 한가지 옵션을 선택하면, 선택된 옵션이 state 변수에 갱신된다.  
```useState```가 어떠한 상태를 갱신하도록 설정되어있는지 확인해보자.  

```javascript
import React, { useState } from "react";
import "./styles.css";

function SelectExample() {
  const [choice, setChoice] = useState("apple");

  const fruits = ["apple", "orange", "pineapple", "strawberry", "grape"];
  const options = fruits.map((fruit) => {
    return <option value={fruit}>{fruit}</option>;
  });

  console.log(choice);

  const handleFruit = (event) => {
    setChoice(event.target.value);
  };

  return (
    <div className="App">
      <select onChange={handleFruit}>{options}</select>
      <h3>You choose "{choice}"</h3>
    </div>
  );
}

export default SelectExample;
```

### Practice - Pop up
Pop up은 open과 close를 state를 통해 관리할 수 있다.
```javascript
import React, { useState } from "react";
import "./styles.css";

function App() {
  const [showPopup, setShowPopup] = useState(false);

  const togglePopup = () => {
    // 클릭을 하면 토글해주자!
    setShowPopup(!showPopup);
  };

  return (
    <div className="App">
      <h1>Fix me to open Pop Up</h1>
      <button className="open" onClick={togglePopup}>
        Open me
      </button>
      {showPopup ? (
        <div className="popup">
          <div className="popup_inner">
            <h2>Success!</h2>
            <button className="close" onClick={togglePopup}>
              Close me
            </button>
          </div>
        </div>
      ) : null}
    </div>
  );
}

export default App;
```

## Controlled Component
React가 state를 통제할 수 있는 컴포넌트를 Controlled Component라고 한다.  
제어 컴포넌트가 동작하는 순서는 아래와 같다.  
- 사용자가 input에 값을 입력한다. 
- 사용자가 값을 입력할 때마다 ```onChange``` 이벤트 핸들러가 발생하여, ```set```메서드를 통해 state 값을 변경한다.
- 변경된 state 값을 input value에 할당한다.

제어 컴포넌트를 사용하면, 입력 값이 생길 때마다 상태를 새롭게 갱신하여 항상 최신값으로 유지할 수 있다.  
즉, 데이터와 UI에서 입력한 값이 항상 동기화 되고 있음을 알 수 있다.  

```javascript
import "./styles.css";
import React, { useState } from "react";

export default function App() {
  const [username, setUsername] = useState("");
  const [msg, setMsg] = useState("");

  return (
    <div className="App">
      <div>{username}</div>
      <input
        type="text"
        value={username}
        onChange={(event) => setUsername(event.target.value)}
        placeholder="여기는 인풋입니다."
        className="tweetForm__input--username"
      ></input>
      <div>{msg}</div>
      <textarea
        placeholder="여기는 텍스트 영역입니다."
        className="tweetForm__input--message"
        onChange={(event) => setMsg(event.target.value)}
        value={msg}
      ></textarea>
    </div>
  );
}
```

## React Data Flow
React의 개발 방식의 가장 큰 특징은 페이지 단위가 아닌, 컴포넌트 단위로 시작한다는 점이다.  
FE 개발자는 앱의 프로토타임을 받으면, 먼저 컴포넌트를 식별한다.  
그렇게 컴포넌트를 만들고, 다시 페이지를 조립해 나간다.  
이러한 개발 방식을 Bottom-Up, 즉 상향식 개발이라고 한다.  
상향식 개발의 큰 장점은 테스트가 쉽고 확장성이 좋다는 점이다.  
  
컴포넌트를 나눌 때에는 단일 책임 원칙에 따라 구분한다.  
하나의 컴포넌트는 한 가지 일만 하도록 하자.  

### Top-Down dataflow
컴포넌트는 컴포넌트 바깥에서 props를 이용해 데이터를 마치 전달인자 (arguments) 혹은 속성 (attrivbutes) 처럼 전달 받을 수 있다.  
데이터를 전달하는 주체는 부모 컴포넌트가 된다.  
이는 데이터 흐름이 Top-Down, 즉 하향식임을 의미한다.  
  
one-way data flow, 단방향 데이터 흐름이 React를 대표하는 키워드일 정도로 이 원칙은 매우 중요하다.  
컴포넌트는 props를 통해 전달받은 데이터가 어디서 왔는지 알지 못한다.  

### State data definition
어플리케이션에서 필요한 데이터가 무엇인지 먼저 정의해야한다.  
변하는 값과 변하지 않는 값이 무엇인가?  
변하는 값들은 state로 정의한다.  
  
다음과 같은 기준으로 state 데이터인지 아닌지 구분해보자.
- 부모로부터 props를 통해 전달되는가?
- 시간이 지나도 변하지 않는가?
- 컴포넌트 안의 다른 state나 props를 가지고 계산가능한가?
이들 중 하나라도 만족한다면 state가 아니다.  

### Location of State
상태가 특정 컴포넌트에서만 유의미하다면, 특정 컴포넌트에만 위치시키면 된다.  
하지만, 만일 하나의 상태를 기반으로 두 컴포넌트가 영향을 받는다면, 이때에는 공통 소유 컴포넌트를 찾아 그곳에 상태를 위치해야 한다.  
즉, 두 개의 자식 컴포넌트가 하나의 상태에 접근하고자 할 때는 두 자식의 공통 부모 컴포넌트에 상태를 위치해야 한다.  

### Reversed Data FLow
부모 컴포넌트에서의 상태가 하위 컴포넌트에 의해 변하는 액션은, 부모의 상태를 변화시켜야 한다.  
하지만, 하위 컴포넌트에서의 클릭 이벤트가, 부모의 상태를 바꿔야만 하는 상황이 있다.  
이를 Lifting state up, State 끌어올리기 라고 한다.  
  
이는 상태를 변경시키는 함수 handler를 하위 컴포넌트에 props로 전달해서 해결할 수 있다.  
이는 마치 콜백 함수를 사용ㅎ아는 방법과 비슷하다.  