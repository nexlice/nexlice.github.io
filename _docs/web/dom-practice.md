---
title: DOM Practice
tags: 
 - DOM
 - fieldset
 - textContent
 - innerText
 - Event Handler
 - Event Object
 - callback
description: Practice with DOM!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

# DOM Practice

## Achievement Goals
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

---

### addEventListener
`addEventListener`는 이벤트에 대해서 하나 이상의 핸들러를 추가할 수 있다.  
- `AJAX` 라이브러리, `JS`모듈, 라이브러리들이 잘 작동한다. 그래서 코드의 확장성이 용이하다.   
- 이벤트에 대한 세밀한 단계를 제공한다.  
    - `캡쳐링`, `버블링`, `패시브`와 같이 단계를 나눠서 조정 가능하다.  
- `HTML`요소 뿐만 아니라 모든 `DOM` 요소에서 작동 가능하다.  
위의 세가지가 너무 중요하다면 `addEventListener`를 쓰는 것이 좋다.    

---

### onclick
그러나 `onclick`은 이벤트 핸들러를 하나밖에 추가하지 못한다.  
하지만 브라우저 호환성을 신경쓴다면 이 방식을 쓰는게 좋다.  

---

### and more...
[MDN web docs](https://developer.mozilla.org/en-US/docs/Web/Events#event_listing)에 가면 이벤트 종류들이 상당히 많다.  

---

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

---

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


