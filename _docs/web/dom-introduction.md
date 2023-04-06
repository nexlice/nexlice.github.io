---
title: DOM Introduction
tags: 
 - DOM
 - Document Object Model
 - Netscape
 - JavaScript
description: Learn about basic DOM!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

# Document Object Model
`DOM`은 `HTMl`요소를 객체; `Object` 또는 `JavaScript Object`처럼 조작할 수 있는 모델이다.  
즉, `JavaScript`를 사용할 줄 알아야 `DOM`으로 `HTML`을 조작할 수 있다.  
정적인 `HTML`을 동적으로 수정가능하게 만든 셈이다..  
  
이렇게 만들어진 구조를 이용하여 `HTML`로 구성된 웹 페이지를 동적으로 움직이게 만들 수 있다.  
이제 조건문, 반복문, 배열, 객체등을 활용할 수 있다!  

---

## Achievement Goals
- `DOM`의 개념을 이해하기
- `DOM`의 구조를 파악하고, `HTML`과 `DOM`이 어떻게 닮아있는지 확인한다.
- `HTML`에서 `JavaScript`파일을 불러올 때 주의점에 대해 이해한다.
    - `<script>`태그가 적용되는 위치에 따라서 실행 결과가 달라질 수 있음을 이해한다.  

---

## Entrance Setting
### Netscape
1998년에 Microsoft를 못이겨 몰락한 회사이다.  
최초의 웹 브라우저 네비게이터였던 `Netscape`는 브라우저의 한 종류이다.  

초창기 웹의 형태는 `HTML` 파일을 화면으로 보여주기만 했다.  
그러다가 웹에 interact를 부여하고자하는 아이디어가 나왔다.  
하지만 이전에는 내컴퓨터 - 모뎀 - 웹페이지 서버 형식으로 통신을 했기 때문에,  
이 모뎀을 통해서 웹페이지 서버와 통신을 하는 통신비가 너무 비싸고 오래걸렸다.  

개발자들은 브라우저가 이걸 전부 해결하면 통신비 문제도 해결할 수 있다고 생각하였다.  
이후 개발자들은 하나의 웹브라우저 상에서 주로 사용하는 프로그래밍 언어를 만들었다.  
그것이 바로 `JavaScript`이다.  

통신비 문제를 결국 이 언어가 해결해주었다.  
이전에는 `JavaScript`라는 이름이 아니라 `모카`였다.  
이름의 변천은 다음과 같다.  
모카 > 라이브 스크립트 > 자바 스크립트 (ECMAscript)  

---

### Browser
`JavaScript`가 등장면서 춘추전국시대가 열렸다.  
통신 문제가 해결되면서 각자 자신들만의 브라우저를 만들었다.  
사파리, 파이어폭스, 오라클, 크롬, 인터넷 익스플로러, 등등, 몇몇은 os에 끼워서 팔기 시작했다.  

각자 자신만의 브라우저를 만들면서 `JavaScript`는 브라우저끼리 호환이 안되게 되어버렸다.  
최대 피해자들은 웹개발자였다.  
호환이 되지 않으므로 다 따로 개발을 해야했기 때문이다.  

---

### Setting Standards
그래서 구글, 마이크로소프트, 파이어폭스같은 큰 기업들이 표준, 규칙을 만들게 되었다.  
브라우저마다 따로따로 개발하지 않도록!!  
그게 현재 `ECMAScript` (ES5, ES6과 같은..) 이다.  
자바가 상표등록이 되어있어서 `JavaScript`라는 이름을 사용하지 못하였다.  
공식 이름은 에크마 스크립트이다.  
그래도 다들 자바스크립트라고 부른다.  

---

#### Why Standards are so important?
표준이 중요한 이유는 무엇인가?  
웹을 빌드하기 위한 것으로 `JavaScript`(`ECMAScript`), `DOM`, `BOM`이 존재한다.  

- BOM : 웹 API로써, 브라우저의 객체를 다루기 위한 속성과 메소드를 제공함.  
- DOM : 웹 API로써, 문서 객체를 다루기 위한 속성과 메소드를 제공함.

브라우저는 `DOM`이라는 규칙을 사용해서 `HTML` 파일을 렌더링한다.  
현재 개발자들도 이 규칙, 기준에 따라 웹을 구현한다.  
따라서 이제 브라우저마다 다르게 코딩을 하지 않아도 된다.  

---

## Applying JavaScript to HTML
이전에도 배웠든 `HTML`에 `JavaScript`를 적용하기 위해서는 `<script>` 태그를 이용한다.  
아래의 경우 `HTML`파일과 같은 디렉토리에 존재하는 `myScriptFile.js`를 불러온다.  

```html
<script scr = "myScriptFile.js"></script>
```

웹 브라우저가 작성된 코드를 해석하는 과정에서 `<script>` 요소를 만나면, 웹브라우저는 `HTML`해석을 잠시 멈춘다.  
`HTML` 해석을 잠시 멈춘 웹브라우저는 `<script>` 요소를 먼저 실행한다.  
**`<script>` 요소는 등장과 함께 실행된다는점을 기억하자.**  

---

### Locations of script tag
- `<head>`에 존재하는 `<script>` 는 다음과 같이 한다.  

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <!-- script 요소 삽입 위치 -->
        <script src="myScriptFile.js"></script>
    </head>
    <body>
        <div id = "msg">Hello JavaScript!</div>
    </body>
</html>
```

- `<body>`가 끝나기 전에 추가하는 `<script>` 

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
    </head>
    <body>
        <div id = "msg">Hello JavaScript!</div>
        <!-- script 요소 삽입 위치 -->
        <script src="myScriptFile.js"></script>
    </body>
</html>
```

두가지 호출 방식에는 어떤 차이점이 있을까?  
`<script>` 요소를 만나면, 웹브라우저는 `HTML`해석을 잠시 멈춘다고 하였다.  
아래 `JavaScript`코드를 잠시 확인하자.  

```javascript
console.log('welcome JavaScript');

let msgElement = document.querySelector('#msg');
console.log(msgElement);
```
두 방식 모두 `myScriptFile.js`내의 첫 번쨰 console.log를 성공적으로 출력하지만,  
두번째 console.log의 경우, `<head>`에 추가한 `<script>`는 제대로 출력하지 못한다.  
따라서 모든 `HTML` 요소가 파싱된 이후, `<body>`의 끝 부분에 `JavaScript`와 연동하는 것을 권장한다.  

---

## Using DOM

`HTML`을 분석하기 위해서 `JavaScript`와 `DOM`을 활용하여 `HTML`에 접근하고 조작한다.  
조건문이나 반복문을 사용할 수 있고, 정보를 저장할 수 있지만, `HTML`에서는 이 모든 게 불가능하다.  

`HTML`을 열고 개발자 도구로 살펴보자.  
```html
<html>
    <body>
        <div id = "nav">
            <div class = "logo"></div>
            <div class = "menu-wrapper">
                <div class = "menu"></div>
                <div class = "menu"></div>
                <div class = "menu"></div>
                <div class = "profile-photo"></div>
            </div>
        </div>
        <div id="news-contents">
            <div class = "news-content-wrapper">
                <div class = "news-picture"></div>
                <div class = "news-title"></div>
                <div class = "news-description"></div>
            </div>
        </div>
        <div id="footer"></div>
    </body>
</html>
```

---

### Implementation of DOM
개발자 도구의 콘솔로 가면 `JavaScript`를 사용할 수 있다.  
자바스크립트에서 `DOM`은 `document` 객체에 구현되어있다.  
브라우저에서 작동되는 `JabaScript` 코드에서는 어디에서나 `document` 객체를 조회할 수 있다.  

---

### console.dir
`DOM` 구조를 조회할 때에는 `console.dir`가 유용하다.  
`console.dir`는 `console.log`와 달리 `DOM`을 객체의 모습으로 출력한다.  

```javascript
conosle.dir(document.body)
```

---

### Child elements
위처럼 조회해보면, 많은 속성이 나타난다.  
`HTML` 엘리먼트에 지정할 수 있었던 다양한 속성이 이미 객체 내에 존재하는 것이다.  
자식들을 찾고싶다면, document.body 객체의 키 중에서 children을 보면 된다.
`console.dir(document.body.children)` 으로 조회해도 된다.  

---

### Parent elements
`document.body.children`을 조회할 때마다 매번 `document.body`로부터 찾아가는 일은 번거롭다.  
따로 변수 선언을 해서 이 정보를 저장해두면, 주소를 참조하기 때문에, 언제든지 접근할 수 있다.  

```javascript
let newsContents = document.body.children[1]
console.dir(newsContents)
```
이제 newContents의 부모 엘리먼트를 가리키는 속성을 `parentElement`로 찾을 수 있다.  

---

### Traversing DOM
`HTML`이 트리구조이기 때문에, `DOM`을 순회하는 것은 결국 트리 구조를 순회하는 것과 같다.  
~~`composite` 패턴이기 때문에 visitor pattern 을 쓰면 되겠다...~~
`DOM` 요소를 순회하는 방법은 [여기](https://www.bsidesoft.com/1431)에서 확인해보자.  

---

## Handling HTML with DOM
CRUD가 가장 중요하다.  
이것을 먼저 이해하고 trivia를 이해하자.  
CRUD는 Create, Read, Update, and Delete를 의미한다.  