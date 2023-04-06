---
title: DOM CRUD
tags: 
 - DOM
 - CRUD
 - Create
 - Read
 - Update
 - Delete
 - querySelector
 - Arraylike
description: Learn about the usage of DOM!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

## Achievement Goals
돔을 자바스크립트로 조작하여 `HTML` 객체를 추가 삭제 변경할 수 있다.  
- Create : `createElement`  
- Read : `querySelector`, `querySelectorAll`  
- Update : `textContent`, `id`, `classList`, `setAttribute`  
- Delete : `remove`, `removeChild`, `innterHTML = ""`, `textContent = ""`  
- APPEND : `appendChild`  
- difference between `innterHTML`, and `textContent`  

---

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