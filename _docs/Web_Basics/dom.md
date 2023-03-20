---
title: DOM
tags: 
 - DOM
 - Document Object Model
 - reset
 - html
 - javascript
description: Learn about basic DOM!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

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

## Achievement Goals _ Intro
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

### Setting Standards
그래서 구글, 마이크로소프트, 파이어폭스같은 큰 기업들이 표준, 규칙을 만들게 되었다.  
브라우저마다 따로따로 개발하지 않도록!!  
그게 현재 `ECMAScript` (ES5, ES6과 같은..) 이다.  
자바가 상표등록이 되어있어서 `JavaScript`라는 이름을 사용하지 못하였다.  
공식 이름은 에크마 스크립트이다.  
그래도 다들 자바스크립트라고 부른다.  

#### Why Standards are so important?
표준이 중요한 이유는 무엇인가?  
웹을 빌드하기 위한 것으로 `JavaScript`(`ECMAScript`), `DOM`, `BOM`이 존재한다.  

- BOM : 웹 API로써, 브라우저의 객체를 다루기 위한 속성과 메소드를 제공함.  
- DOM : 웹 API로써, 문서 객체를 다루기 위한 속성과 메소드를 제공함.

브라우저는 `DOM`이라는 규칙을 사용해서 `HTML` 파일을 렌더링한다.  
현재 개발자들도 이 규칙, 기준에 따라 웹을 구현한다.  
따라서 이제 브라우저마다 다르게 코딩을 하지 않아도 된다.  

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
### remove
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
`innerHTML`은 `string`을 파싱해서 엘리먼트로 변환하여 집어넣는 속성이다.  
이 메서드를 이용해서 모든 자식 엘리먼트를 지울 수도 있다.  

하지만 이 메서드를 통해서 값을 삽입할 수 있는데,  
`string` 자체를 가리지 않고 파싱하고 넣는다는 점에서 보안 문제가 발생한다.  
따라서 textContent를 보안상의 이유로 더 권장한다.  
```html
<div>악의적 코드</div>
```
`innerHTML`을 사용하면 저 코드를 남의 웹에 넣어서 정보를 탈취할 수도 있다.  
그래서 `innerHTML`을 권장하지 않고 대신할 다른 메서드를 권장한다.  


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

# DOM Practice
## Achievement Goals _ DOM Practice
- onclick, onkeyup, addEventListener 메서드로 이벤트 핸들러 함수를 `HTML` 엘리먼트에 적용할 수 있다.
    - 이벤트 핸들러 함수에서 이벤트가 발생한 곳의 정보를 확인할 수 있다.
    - 이벤트 핸들러 함수로 유효성 검사를 실행할 수 있다.
    - 유효성 검사에 필요한 기술 요소를 익힌다.
    - 유효성 검사에 필요한 `HTML` 엘리먼트, `CSS`속성이 무엇인지 알 수 있다.
- 엘리먼트가 화면에 표시되거나 사라지게 만들 수 있다; `display: none`
    - 유효성 검사에서 활용할 수 있는 정규표현식 사용법 기초에 대해서 익힌다.
- 관심사 분리를 적용하거나 유효성 검사 함수를 따로 분리해서 설계한다.
- 기초적인 이벤트를 알고, 이벤트 핸들러를 엘리먼트에 적용할 수 있다.
    - `onlick` event
    - `onclick`에 직접 할당하는 것과 `addEventListener`의 차이
    - eventHandler 함수를 만들고, eventHandler의 첫번째 인자를 사용할 줄 안다.

---

## fieldset
`<fieldset>` 태그는 `<form>` 요소에서 연관된 요소들을 하나의 그룹으로 묶을 때 사용한다.  
`<fieldset>` 요소는 하나의 그룹으로 묶은 요소들 주변으로 박스 모양의 선을 그려준다.  
또한, `<legend>` 요소를 사용하면 `<fieldset>` 요소의 캡션(caption)을 정의할 수 있다.  

---

## textContent vs value
|특징|textContent|value|
|:---:|:---:|:---:|
|공통점| `text` 값을 가져와서 변경|
|차이점|`textContent`는 `Node`의 속성|`input`과 같은 `form` 요소의 값을 가져오고 싶을 때 사용|

---

### textContent
`innetText`와는 달리 `<script>`나 `<style>` 태그와 상관없이. 해당 노드가 가지고 있는 텍스트 값을 그대로 읽는다.  
또한 연속된 공백이 그대로 보여진다.  
`'display:none'` 스타일이 적용된 `'숨겨진 텍스트'` 문자열도 그대로 출력된다.  

---

### innerText
`innerText`는 `Element`의 속성이다.  
해당 `Element` 내에서 사용자에게 **보여지는** 텍스트 값을 읽어온다.  
내용에 연속되는 공백이 있다면, 연속 공백을 무시하고 하나의 공백만 처리하여 보여진다.  
`display : none` 한 값들은 불러들이지 않는다.  

---

## Event Handler
컴퓨터는 이벤트가 발생하는 시점을 알 수 없다. (사용자가 언제 이벤트를 발생 시킬 지 알 수 없다.)
그래서 이벤트(사용자의 상호작용)가 발생하면, 그 이벤트를 감지를 해서 처리해줄 수 있도록, 함수를 미리 등록한다.  
```javascript
.onclick(function(){
    //일련의 처리 과정
})
```
이 함수를 `Callback Function` (`Event Handler`. 이벤트를 handle하는 역할)라고 하고,  
`Event Listener`에 `Callback Function`을 등록한다고 한다.  

---

## Event Object
웹에서 클릭이나 드래그하는 일을 이벤트라고 한다.  
이벤트와 이벤트 핸들러를 엘리먼트에 적용하여, 사용자가 엘리먼트에 특정 이벤트를 발생시켰을 때, 이벤트 핸들러가 동작하도록 하자.  

```javascript
// 모든 버튼을 가져온다.
let menus = document.querySelectorAll("button");

let btnAmericano = menus[0];
let btnCaffelatte = menus[1];

btnAmericano.onclick = handleClick;
btnCaffelatte.onclick = handleClick;


function handleClick(){
    // 문자열은 엘리먼트 안의 값, contents안에 들어가 있다.
    let currentMenu = "";
    console.log(currentMenu + "를 클릭하셨습니다.");
}
```

---

## Attaching Callback Function
```javascript
// 예전 방식
divElement.onClick = () => {} 
// 최근 방식
divElement.addEventListener('click', () => {}) 
```
브라우저와의 호환성 때문에 예전 방식을 사용할 수 있다.  

### addEventListener
`addEventListener`는 이벤트에 대해서 하나 이상의 핸들러를 추가할 수 있다.  
- `AJAX` 라이브러리, `JS`모듈, 라이브러리들이 잘 작동한다. 그래서 코드의 확장성이 용이하다.   
- 이벤트에 대한 세밀한 단계를 제공한다.  
    - `캡쳐링`, `버블링`, `패시브`와 같이 단계를 나눠서 조정 가능하다.  
- `HTML`요소 뿐만 아니라 모든 `DOM` 요소에서 작동 가능하다.  
위의 세가지가 너무 중요하다면 `addEventListener`를 쓰는 것이 좋다.    

### onclick
그러나 `onclick`은 이벤트 핸들러를 하나밖에 추가하지 못한다.  
하지만 브라우저 호환성을 신경쓴다면 이 방식을 쓰는게 좋다.  

### and more...
[MDN web docs](https://developer.mozilla.org/en-US/docs/Web/Events#event_listing)에 가면 이벤트 종류들이 상당히 많다.  

## Practice 1
이제 아래 `HTML` 구조를 `DOM`을 이용해 만들 수 있다.
```html
<body>
    <div class = "tweet">
        <div class="username"></div>
    </div>
</body>
```


```javascript
let tweetDiv = document.createElement("div");
tweeDiv.classList.add("tweet");

let usernameDiv = document.createElement("div");
usernameDiv.classnList.add("username"):
usernameDiv.textContent = "나원후";

tweetDiv.append(usernameDiv);

/* body에 append 해야 보인다! */
document.body.append(tweetDiv);
```

## Practice 2
이벤트 핸들러를 붙여 클릭한 요소가 무엇인지 콘솔에 나오도록 하자.  
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- 처음부터 치지 말고 태그이름#id이름 치면 바로 된다.-->

    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>이벤트 객체</title>
  </head>
  <body>
    <button>아메리카노</button>
    <button>카페라떼</button>
    <script>
      let menus = document.querySelectorAll("button"); //모든 버튼을 가져옵니다.

      let btnAmericano = menus[0];
      let btnCaffelatte = menus[1];

      function handleClick() {
        // 아래의 빈 칸(____)을 채우세요.
        // console.log("working?");
        console.log(event.target.textContent)
        let currentMenu = event.target.textContent; // TODO
        console.log(currentMenu + "를 클릭하셨습니다.");
      }

      btnAmericano.onclick = handleClick;
      btnCaffelatte.onclick = handleClick; // 이상으로 for 문으로 충분히 구현할 수 있는 내용입니다.
    </script>
  </body>
</html>

```
---

## Further Study
- The difference between element and node
- The difference between children and childNodes in javascript dom
- The difference between remove and removeChild in javaScript dom
    - remove : 반환값이 없다. 자식 레벨에서 접근해도 노드 삭제가 가능
    - removeChild : 반환 값이 있다. 부모레벨에서 접근해야 노드 삭제가 가능
- The difference between append and appendChild
    - append : 여러개의 자식 엘리먼트를 동시에 추가 가능  
    - appendChild : 한 번에 하나의 자식 엘리먼트 추가 가능  
- The difference between innerHTML and textContent
    - innter HTML : string을 파싱해서 엘리먼트로 변환하여 집어넣는 속성 
    - textContent : 엘리먼트 내 content부분에 텍스트만 넣어주는 메서드.  
- tweets에 forEach는 되는데, reduce 는 안되는 이유 (why array method is nor working on nodelist)
- tweets를 유사배열에서 배열로 바꾸는 방법 (how to convert nodelist into javascript array)
- 같은 element를 appendChild하면 기존 엘리먼트를 복사하는가? 
- createDocumentFragment
- HTML5 template tag
- offsetTop, offsetWidth

- 이벤트 객체란 무엇인가?
    - 웹과 사용자가 상호작용을 할 수 있도록 만들어주는 것.  
    - 인터렉티브한 활동을 할 수 있도록 돕는 장치.  
- 이벤트 객체에는 어떤 내용이 출력되는가?  
- `event.target`은 어떤 값을 담고 있는가 : 해당 이벤트의 `HTML` 엘리먼트를 가져온다.
- onsubmit, onchange, onmouseover, onkeyup, event.preventDefault  


