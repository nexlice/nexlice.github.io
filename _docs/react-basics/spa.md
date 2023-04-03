---
title: React SPA
tags: 
 - React
 - Wireframe
 - SPA
 - Router
 - Browse Router

description: Learn about basic React!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->


# React SPA
## Achievement Goals
- `SPA` (Single-Page Application) 개념을 이해하고 설명할 수 있다.  
- SPA의 장, 단점에 대해 이해하고 설명할 수 있다.  
- 와이어 프레임을 보고 어느 부분을 컴포넌트로 구분해야 할지 스스로 정할 수 있다.  
- React에서 npm으로 React Router DOM을 설치 (`npm install react-router-dom`)하고 이용할 수 있다.  
- React Router DOM을 이용하여 SPA를 구현할 수 있다.  
- 라우팅 구조를 짤 수 있어야 하고, 이에 필요한 기초 문법들을 사용할 수 있어야 한다.  

## Entrance Setting
전통적인 웹사이트에서는 사용자가 웹사이트 내의 다른 페이지로 이동하면,  
브라우저가 페이지를 보여주기 위해 매번 HTML파일로 된 "페이지 전체"를 불러와야만 했다.  

### 전통적인 웹사이트의 한계와 단점
웹사이트가 보다 복잡해지고 애플리케이션의 형태를 가지게 되면서, 사용자와 서비스 사이에 더욱 많은 상호작용이 일어나게 되었다.  
하지만 이때마다 Header나 Navigation Bar 등과 같이 중복되는 요소들을 매번 불러오는 것이 깜빡이는 현상을 일으키며 서버와의 불필요한 트래픽을 발생시켰다. (`SSR`)  
한편, 사용자 입장에서는 매번 모든 페이지를 불러옴에 따라 더 느린 반응성을 갖게 되었고, 이는 애플리케이션과 같은 사용자 경험을 제공하기 어렵게 만들었다.  

### SPA의 둥장
1990년대 후반에 HTML 문서 전체가 아닌, 업데이트에 필요한 데이터만 서버에서 전달받아,  
이 데이터를 `JavaScript`가 동적으로 `HTML` 요소를 생성해서 화면에 보여주는 방식이 개발되어 사용되기 시작하였다.  
2000년대 중반부터 이러한 개발 방식을 이용한 웹 애플리케이션이 보편화되었으며, 이것이 `SPA`이다.  

## SPA
SPA는 서버로부터 완전히 새로운 페이지를 불러오는 것이 아니라,  
화면을 업데이트하기 위해 필요한 데이터만 서버에서 전달받아,  
브라우저에서 해당하는 부분만 업데이트 하는 방식으로 작동하는 웹 애플리케이션이나 웹사이트를 말한다.  

### Pros
애플리케이션과 사용자 사이에 수시로 상호작용이 발생하는데,  
이때 페이지 전체를 렌더링하는 것이 아니라, 필요한 부분만 업데이트 하기 때문에,  
SPA는 사용자의 행동에 빠르게 반응한다.  
서버 입장에서는 요청받은 데이터만 넘겨주면 되기 때문에, 과거와 같은 과부하 문제도 현저히 줄일 수 있다.  
또한 화면 전체를 새로 렌더링할 필요가 없기 때문에, 보다 나은 사용자 경험을 제공한다.  
이런 SPA 방식으로 만들어진 대표적인 서비스로는 Youtube가 있다.  
이 밖에 facebook, airbnb, Netflix 등,  
우리가 일상적으로 사용하는 다양한 서비스들이 SPA 방식으로 제작되어 있다.  

### Cons
- 느린 첫 화면 로딩 시간  
브라우저는 첫 화면 로딩 시에 HTML 파일을 읽어들인 후,  
그 안의 script 요안에 있는 JavaScript 파일을 다시 받아오는 과정을 거친다.  
이때 첫 화면 로딩 시 읽어들인 HTML 파일은 거의 비어있고,   
대부분의 코드는 JavaScript 파일 안에 들어있다 보니, 자연스럽게 JavaScript 파일이 무거워진다.  
때문에 이 JavaScript 파일을 기다리는 시간으로 인해 첫 화면의 로딩 시간이 길어진다.  

- 검색 엔진 최적화  
검색 엔진 최적화란 구글이나 네이버 같은 검색엔진이 자료를 수집하기 좋도록 웹 페이지를 구성하는 것을 뜻한다.  
여기서 검색 엔진의 작동 방식을 잠깐 알아보면,  
검색 로봇이 웹 페이지에 있는 정보를 수집하고 분석해서,  
그 결괏값에 인덱스를 만들어 보관하고 있다가,  
사용자가 검색어를 입력하면,  
보관하고 있던 인덱스에서, 검색어와 가장 연관성이 높은 웹 페이지들은 순서대로 보여주는 방식으로 작동한다.  
검색 로봇은 자료를 수집할 때에 웹 페이지의 URL은 물론이고,  
HTML 문서 내의 각종 태그나 링크 등을 분석한다.  
SPA는 HTML이 거의 비어있다 보니 검색 로봇이 충분한 자료를 수집하지 못한다.  
이 때문에 검색 노출이 중요한 웹 애플리케이션은, 검색 엔진 최적화에 대한 대응책을 따로 마련해야 하고,  
더불어 앱 안에서 브라우저의 앞으로 가기/뒤로 가기 등의 상태 관리도 해야하기 때문에, 개발의 복잡도가 더욱 늘어난다.  
다만 SPA에서도 검색 엔진 최적화에 대응할 수 있도록 검색 엔진이 발전하고 있어서, 점차 이 단점은 사라지고 있는 추세이다.  

## Wireframe
React에서 컴포넌트를 어떻게 나누어야할까? 그리고 컴포넌트를 나누는 것이 왜 중요할까?  

### Wireframe과 Mockup
Wireframe은 디자인에 들어가기 전 단계로 선(`wire`)를 이용해 윤곽선(`frame`)을 잡는 것을 말한다.  
이 작업을 통해 개발자는 디자인 컨셉과 사이트 기능에 대한 이해를 할 수 있다.  
그리고 목업(`Mockup`)은 데스크탑, 스마트폰의 프레임을 덧씌워 직관적으로 이해하기 쉽게 디자인한 것을 말한다.  

## React Router
SPA는 하나의 페이지를 가지고 있지만 사실 한 종류의 화면만 사용하지 않는다.  
이를테면 Twilttler와 같은 SPA를 만들 때,  
메인 트윗 모음 페이지, 알림 페이지, 마이 트윗 페이지 등의 화면이 필요할 수 있다.  
또한 화면에 따라 "주소"도 달라진다.  
이렇게 다른 주소에 따라 다른 뷰를 보여주는 과정을 "경로에 따라 변경한다."라는 의미로 라우팅(Routing)이라고 한다.  
하지만 리엑트 자체에는 이 기능이 내장되어 있지 않다.  
> React SPA에서는 라우팅을 위해 React Router라는 라이브러리를 가장 많이 사용한다.  

### React Router 주요 컴포넌트
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

### Environment Setting
npm 명령어를 통해 간단하게 설치 가능하다.
```bash
npm install react-router-dom@^6.3.0
```

## React Router Tutorial
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
### BrowseRouter
`BrowseRouter`는 웹 애플리케이션에서 HTML5의 API를 사용해,  
페이지를 새로고침하지 않고도 주소를 변경할 수 있는 역할을 해준다.  
아래와 같이 ReactDOM의 렌더 단계인 index.js에 넣어서 활용할 수도 있다.  
`BrowseRouter`가 상위에 작성되어 있어야 Route 컴포넌트를 사용할 수 있다.  

### index.js
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowseRouter } from 'react-router-dom';

ReactDOM.render(<BrowserRouter><App/></BrowserRouter>, document.querySelector('#root'));
```

### Routes, Route
경로를 매칭해주는 역할을 하는 컴포넌트이다.
- `<Routes>`  
여러 `<Route>` 를 감싸서 그 중 경로가 일치하는 단 하나의 라우터만 렌더링을 시켜주는 역할을 한다. 
`<Routes>` 를 사용하지 않으면 매칭되는 모든 요소를 렌더링 한다.  
- `<Route>`  
path와 element 속성을 지정하여 해당 path에 어떤 컴포넌트를 보여줄지 정한다.  
아래에서 나오는 Link 컴포넌트가 정해주는 URL 경로와 일치하는 경우에만 작동한다.

### Link
경로를 연결해주는 역할을 하는 컴포넌트이다.  
페이지 전환을 통해 페이지를 새로 불러오지 않고 애플리케이션을 그대로 유지하여,  
HTML5 History API를 이용해 페이지의 주소만 변경해준다.  
ReactDOM으로 렌더를 시키게되면 `<Link>` 컴포넌트는 `<a>` 태그로 바뀐다.  

> React Router에서 `<a>` 태그가 아닌 `<Link>` 를 사용하는 이유는?  

`<a>` 태그는 페이지를 전환하는 과정에서 페이지를 불러오기 때문에 다시 처음부터 렌더링을 시킨다.  
즉, 새로고침 현상이 일어난다.  
하지만 ```<link>``` 컴포넌트는 **페이지 전환을 방지하는 기능이 내장**되어있기 때문에 SPA를 구현할 수 있다.