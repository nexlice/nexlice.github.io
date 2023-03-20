---
title: DOM
tags: 
 - DOM
 - Document Object Model
 - reset
 - html
 - javascript
description: Learn about basic git commands!
---

# DOM Introduction
`DOM`은 프로그래머 관점에서 바라 본 `HTML`이다.  
`DOM`을 이해하고 조작할 수 있다면, `HTML`을 단순한 문서에서 웹 앱으로 업그레이드 할 수 있다.  
`DOM`은 브라우저 환경에서 `JavaScript`를 이용해 `HTML`을 조작할 수 있다.  
`HTML`문서에 이미 작성되어있는 엘리먼트에 접근하거나, 새로운 엘리먼트를 생성 또는 삭제가능하다.  

--- 

## Document Object Model
`DOM`은 `HTMl`요소를 객체; `Object` 또는 `JavaScript Object`처럼 조작할 수 있는 모델이다.  
즉, `JavaScript`를 사용할 줄 알아야 `DOM`으로 `HTML`을 조작할 수 있다.  
정적인 `HTML`을 동적으로 수정가능하게 만든 셈이다..  
  
이렇게 만들어진 구조를 이용하여 `HTML`로 구성된 웹 페이지를 동적으로 움직이게 만들 수 있다.  
이제 조건문, 반복문, 배열, 객체등을 활용할 수 있다!  

---

## Achievement Goals - Intro
- `DOM`의 개념을 이해하기
- `DOM`의 구조를 파악하고, `HTML`과 `DOM`이 어떻게 닮아있는지 확인한다.
- `HTML`에서 `JavaScript`파일을 불러올 때 주의점에 대해 이해한다.
    - `<script>`태그가 적용되는 위치에 따라서 실행 결과가 달라질 수 있음을 이해한다.  

---

## Applying JavsScript to HTML
이전에도 배웠든 `HTML`에 `JavaScript`를 적용하기 위해서는 `<script>` 태그를 이용한다.  
아래의 경우 `HTML`파일과 같은 디렉토리에 존재하는 `myScriptFile.js`를 불러온다.  

```html
<script scr = "myScriptFile.js"></script>
```

웹 브라우저가 작성된 코드를 해석하는 과정에서 `<script>` 요소를 만나면, 웹브라우저는 `HTML`해석을 잠시 멈춘다.  
`HTML` 해석을 잠시 멈춘 웹브라우저는 `<script>` 요소를 먼저 실행한다.  
**`<script>` 요소는 등장과 함께 실행된다는점을 기억하자.**  

---

### Locations of \<script\>
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

# Handling HTML with DOM
CRUD가 가장 중요하다.  
이것을 먼저 이해하고 trivia를 이해하자.  
CRUD는 Create, Read, Update, and Delete를 의미한다.  

---
## Achievement Goals _ CRUD
돔을 자바스크립트로 조작하여 `HTML` 객체를 추가 삭제 변경할 수 있다.  
- Create : `createElement`  
- Read : `querySelector`, `querySelectorAll`  
- Update : `textContent`, `id`, `classList`, `setAttribute`  
- Delete : `remove`, `removeChild`, `innterHTML = ""`, `textContent = ""`  
- APPEND : `appendChild`  
- difference between `innterHTML`, and `textContent`  

## Create
```javascript
//Create an element
const a = document.createElement('div');

//Allocate to the body
document.body.append(a);
```
적절한 위치에 넣기 위해서는, 구조를 보고 옳은 위치에 넣어야한다.  
적절한 위치를 찾기 위해서 순회를 하는 방법도 있지만, 더 좋은 방법이 있다.  


---

## Read

### querySelector
`JavaScript`의 원시 자료형인 변수의 값을 조회할 떄, 변수의 이름으로 직접 조회가능하다.  
참조 자료형인 `Array`는 `index`를, `Object`는 `key`를 이용해 값을 조회한다.  
그러나 `DOM`은 조금 특별한 방법을 사용한다.  
`DOM`으로 `HTML` 엘리먼트의 정보를 조회하기 위해서는, `querySelector`의 첫 번쨰 인자로 `selector`를 전달하여 확인 가능하다.  
셀렉터로는 html `<div>` 따위의 것, `id "#tweetList"`, `class ".tweet"`을 가장 많이 사용한다.  

---

### querySelectorAll
여러 엘리먼트를 한 번에 가져오기 위해서는, `querySelectorAll`을 사용한다.  
이렇게 조회한 `HTML` 엘리먼트들은 배열처럼 `for loop`를 사용할 수 있다.  

---

### Array like object
하지만 앞서 조회한 `HTML` 엘리먼트들은 배열이 아니다.  
"배열이 아닌 배열"을 `유사 배열`, `배열형 객체` 등 다양한 이름으로 부른다.  
정식 명칭은 `Array-like-Object`이다.  

---

#### Compatibility
호환성을 위해서 옛날 메서드를 사용해야하기도 한다.  
```javascript
document.getElementById

// 이 메서드는 ducument.querySelector와 정확히 같은 일을 수행한다.  
```

---

### classList
 `JavaScript`로 만든 엘리먼트를 append하면 `class`가 정의되어있지 않아, `CSS`의 스타일링이 적용되지 않는다.  
클래스를 추가하기 위해서 다음과 같이 한다.  
```javascript
oneDiv.classList.add('tweet')
```

---

## Update
내용을 넣기 위해서는 update를 한다.  
해당 객체의 `textContent = "내용"`을 통해서 값을 넣어주자.  

특정 클래스에 추가할때에는 다음과 같이도 가능하다.
```javascript
const container = document.querySelector('#container')
container.append(oneDiv)
```

`class`, `id` 말고 다른 attribute를 추가하기위해서는 `setAttribute`를 사용하자.  

---

## Delete
### 위치를 알고있는 경우
```javascript
const container = document.querySelector('#container')
const tweetDiv = document.createElement('div')
container.append(tweetDiv)
tweetDiv.remove()
```
  
---

### innerHTML
```javascript
document.querySelectore('#container').innerHTML = '';
```
모든 자식 엘리먼트를 지운다는 점에서 보안 문제가 발생한다.  
그래서 `innerHTML`을 권장하지 않고 대신할 다른 메서드를 사용한다.  


---

### removeChild
`innerHTML`과 같은 일을 수행한다; 자식 엘리먼트를 지정해서 삭제한다.  
모든 자식 엘리먼트를 삭제하기 위해 반복문을 활용할 수 있다.  
다음 코드는 자식 엘리먼트가 남아있지 않을 때까지 첫번째 자식 엘리먼트를 삭제하는 코드이다.  

```javascript
const container - dociment.querySelector('#container');
while (container.fisrtChild){
    container.removeChild(container.firstChild)
}
```
이 방식으로 요소를 삭제하면 제목에 해당하는 `h2 "TweetList"`까지 삭제된다.  
이를 방지하기위해 여러 요소를 사용할 수 있다.  
이를테면 문자열을 비교해 `tweet List`만 남기거나,  
새로운 변수를 생성하고 `tweet List`를 할당해뒀다가 반복문이 끝나면 새롭게 추가하거나,  
또는 자식 엘리먼트를 하나만 남기게 할 수 있다.  

```javascript
const container = document.querySelector('#container');
while (container.children.length > 1){
    container.removeChild(container.lastChild);
}
```

또는 직접 클래스 이름이 `tweet`인 엘리먼트만 찾아서 지울 수 있다.  
```javascript
const tweets = dociment.querySelectorALL('.tweet')
tweets.forEach(function(tweet)){
    tweet.remove();
}
```

---

## Further Study
- the difference between element and node
- difference between children and childNodes in javascript dom
- difference between removeChild and remove in javaScript dom
- tweets에 forEach는 되는데, reduce 는 안되는 이유 (why array method is nor working on nodelist)
- tweets를 유사배열에서 배열로 바꾸는 방법 (how to convert nodelist into javascript array)
- 같은 element를 appendChild하면 기존 엘리먼트를 복사하는가? 
- createDocumentFragment
- HTML5 tempate tag
- offsetTop. offsetWidth