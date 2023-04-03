---
title: Async
tags: 
 - async
 - sync
 - blocking
 - non blocking
 - JavaScript
 - Node.js
 - callback
 - promise
 - async/await
 - module

description: Learn about the concept of Async!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->


# Async

## Achievement Goals
- 중첩된 callback의 발생
- nested callback vs Promise
- Promise
    - `resolve`, `reject`, `then`, `catch`
    - parameters
    - 3 states
    - `Promise.all`
- `async/await`
- `fs`

## Asynchronous Call
Javascript안에서 비동기/동기 호출에 대해서 알아보자.

### callback
다른 함수의 parameter로 넘겨주는 함수이다.  
parameter를 넘겨받는 함수 A는 callback 함수 B를 필요에 따라 즉시 실행(synchronously)할 수도 있고,  
나중에 (asynchronously) 실행할 수도 있다.  

```javascript
function B(){
    console.log('called at the back!');
}

function A(callback){
    callback();
}

A(B);
```
#### 어디에서 사용하는가?
- iterator : map에 들어가는 콜백 함수는 반복적으로 실행된다
- event handler : 이벤트가 생기면 호출된다.

#### Precautions
콜백 함수를 연결할 때 함수 실행을 연결하는 것이 아닌, 함수 자체를 연결해야한다.  

```javascript
// 틀린 예
document.querySelector('#btn').onclick = handleClick();

// 옳은 예
document.querySelector('#btn').onclick = handleClick;
```

### blocking vs non blocking
- blocking : 하던 일을 멈추고 받아야 한다  
- synchronous : 요청에 대한 결과가 동시에 일어난다  
- non blocking : 확인 후, 나중에 답장할 수 있다  
- asynchronous : 요청에 대한 결과가 동시에 일어나지 않는다  

> 응답을 주는 것은 트리거가 생기면 발생하는 이벤트에 해당한다.

## Examples

**synchronous의 예**  

```javascript
// ms 범위 내에서 무한 루프를 도는 blocking 함수
function waitSync(ms){
    var start = Date.now();
    var now = start;
    while(now - start < ms) {
        now = Date.now();
    }
}

function drink(person, coffee) {
    console.log(person + '는' + coffee + '를 마십니다');
}

function orderCoffeeSync(coffee){
    console.log(coffee + '가 접수되었습니다');
    waitSync(2000);
    return coffee;
}

let customers = [{
    name : 'Steve',
    request : '카페라떼'
}, {
    name : 'John'.
    request : '아메리카노'
}];

// call synchronously
customers.forEach(function(customer){
    let coffee = orderCoffeeSync(customer, request);
    drink(customer.name, coffee);
});
```

**결과**  
```bash
카페라떼가 접수되었습니다
Steve는 카페라뗴를 마십니다
아메리카노가 접수되었습니다
John는 아메리카노를 마십니다
```

**asynchronous의 예**  
```javascript
// 특정 시간 이후에 callback 함수가 실행되게끔 하는 브라우저 내장 함수
function waitAsync(callback, ms){
    setTimeout(callback, ms);
}

let customers = [{
    name : 'Steve',
    request : '카페라떼'
}, {
    name : 'John'.
    request : '아메리카노'
}];

function orderCoffeeASync(menu, callback){
    console.log(menu + '가 접수되었습니다');
    waitAsync(function(){
        callback(menu);
    }, 2000)
}

// call asynchronously
customers.forEach(function(customer){
    orderCoffeeAsync(customer.request, function(coffee){
        drink(customer.name, coffee);
    });
});
```

## Forwarding async functions
```javascript
// callback 패턴
let request = 'caffelatte';
orderCoffeeAsync(request, function(response){
    drink(response);
});

// 이벤트 등록 패턴
let request = 'caffelatte';
orderCoffeeAsync(request).onready = function(response){
    drink(response);
};
```

즉, 동기, synchronous는 직렬적 수행이고, 비동기 asynchronous는 병렬적 수행이다.  

### Prime usage of async functions
- DOM Element의 이벤트 핸들러
    - onclick, keydown
    - page loading
- Timer
    - TimerAPI : setTimeout
    - AnimationAPI : requestAnimationFrame
- Server request
    - fetch API
    - AJAX (XHR)

## Why Async
`Node.js`는 `asynchronous event-driven JavaScript runtime`이며, thread없이 디자인 되었다.  
동기적 : 클라이언트가 서버에게 요청을 보냈을 때, 서버가 요청을 받는 상황에서 클라이언트는 아무것도 하지 않고 기다린다.  
서버가 응답을 보내면 그때부터 클라이언트는 일을 한다.  
비동기적 : 클라이언트가 서버에게 요청을 한 이후에도 자신의 일을 한다.  

이를테면 YouTube를 볼 때 영상이 로드 되는 동안 아무것도 못한다고 한다면 동기적이다.  
로딩 되는 동안 다른 활동을 할 수 있다면 비동기적이다.  

로딩이 되는동안 사용자의 행동이 제한되면 UX를 크게 떨어뜨린다.  
이러한 이유에서 비동기를 사용한다.  

## Controlling Async
비동기로 여러 태스크를 할 때, 각각의 태스크가 걸리는 시간이 다를 수 있기 때문에, 결과를 실행시간에만 알 수 있다.  
만약 이 실행 순서를 제어하고 싶다면, 어떻게 해야할까?  

### callback
async를 handling하기 위해서 callback을 사용한다.  
`A를 다 실행하면 B 호출해줘` 의 꼴.  

#### callback hell
순차적으로 이뤄져서 좋긴한데, 가독성도 떨어지고 코드 관리가 힘들어진다.

### Promise
`promise`는 프로미스가 생성된 시점에는 알려지지 않았을 수도 있는 값을 위한 대리자이다.  
비동기 연산이 종료된 이후에 결과 ㄱ밧과, 실패 사유를 처리하기 위한 처리기를 연결할 수 있다.  
프로미스를 사용하면 비동기 메서드에서 마치 동기 메서드처럼 값을 반환할 수 있다.  
하지만 최종 결과를 반환하는 것이 아니고, (런타임에 결정)  
미래의 어떤 시점에 결과를 제공하겠다는 `약속`을 제공한다.   

#### promise의 3가지 상태
- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
    resolve, reject가 정해지기 전 상태.  
    new Promise(); 이렇게만 호출하면 대기 상태가 된다.

- Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 겨로가 값을 반환해준 상태
    콜백 함수의 인자 resolve를 실행하면 Fulfilled 상태가 된다.
    resolve();
    이행 상태가 되면 then()을 이용하여 처리 결과 값을 받을 수 있다.
    .then{
        console.log(resolvedData);
    }
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태
    콜백 함수의 인자 reject를 실행하면 Rejected 상태가 된다.
    reject();
    실패 상태가 되면, 실패한 이유(실패 처리의 결과 값)을 catch()로 받을 수 있다.
    .catch(function(err){
        console.log(err);
    })

#### promise.all
Promise안의 값을 사용하기 위해서 사용한다.

#### resolve vs reject
<!-- https://ko.javascript.info/async-await -->
```javascript
new Promise(function (resolve, reject) {
    resolve(data);
    reject(new Error("error!"));
})
// resolve() : Promise 실행 함수 내의 작업이 성공했을 때 수행된다.
// 파라미터를 넣어주다면 전달할 값을 파라미터로 넣어준다.  

// reject() : Promise 실행 함수 내의 작업이 실패했을 때 수행된다.
// 파라미터를 넣어준다면 에러 객체를 넣어준다.
// 결과 값은 then이나 catch에서 받을 수 있다.
```

#### resolve의 인자가 하는 역할
resolve를 호출할 때 특정 값을 파라미터로 넣으면, 이 값을 작업이 끝나고 사용할 수 있다.    
`.then(param)`을 통해서 사용 가능하다.  

#### then, catch
resolve가 되면 then으로 넘어가고, reject가 되면 catch로 넘어간다.

### callback vs promise
Callback Hell을 벗어나기 위해서 사용한다. Promise는 클래스이다.  
다음과 같은 callback hell이 있다고 하자.  

```javascript
const printString = (string, callback) => {
    setTimeout(
        () => {
            console.log(string)
            callback()
        },
        Math.floor(Math.random() * 100) + 1
    )
}

const printAll = () => {
    printString("A", () => {
        printString("B", () => {
            printString("C", () => {})
        })
    })
}

printAll() // always prints ABC
```

Promise를 활용한다면 다음과 같이 변화시킬 수 있다.
```javascript
const printString = (string) => {
    // promise는 자신만의 callback을 받는다.
    return new Promise((resolve, reject) => {
        setTimeout(
           () => {
                console.log(string)
                // 받은 함수를 실행
                resolve()
            },
            Math.floor(Math.random() * 100) + 1
        )

        //에러 처리를 하고 싶다면 try catch를 통해 reject함수를 사용한다.
    })
}

const printAll = () => {
    printString("A")
    // then : printString이 끝나면 실행해줘
    .then(() => {
        return printString("B")
    })
    .then(() => {
        return printString("C")
    })
    // reject 처리를 했다면 이곳에 .catch를 하기도 한다.
    // chaining 과정에서 마지막에 .catch를 함으로써
    // 어디서 에러가 나더라도 에러 핸들링이 가능하다.
    // >> 에러핸들링을 매 콜백 시점마다 할 필요가 없다.
}

printAll() // always prints ABC
```

#### but..
하지만 `promise`를 활용할지라도 `return` 문을 사용하지 않으면, `promise hell`이 생길 수 있다.  

### aysnc wait
JS 비동기 처리를 원활하게 하기 위해 ES7에서 추가된 JS문법.  
await는 최상위 렙레에서 사용할 수 없고, (익명) 함수 안에서 사용해야 한다.  
즉, async/wait은 promise와 동일한 기능을 하지만, syntactic 추가이다.  
비동기 함수를 마치 동기적인 프로그램인 것처럼 보이게할 수 있다.  
함수 앞에 async를 붙이면 해당 함수는 항상 promise를 반환한다.
promise가 아닌 값을 반환하더라도, 이행 상태의 프로미스 (resolved promise)로 값을 감싸,
이행된 promise가 반환 되도록 한다.

#### await 키워드를 사용했을 때의 리턴값
await은 Promise 객체나 그 객체를 반환하는 함수 앞에만 사용할 수 있다.  

#### await 키워드 다음에 등장하는 함수 실행의 리턴 타입
JavaScript는 await 키워드를 만나면 promise가 처리될 때까지 기다린다.  
결과는 그 이후 반환된다.  
즉, await 키워드 다음에 등장하는 함수 실행의 리턴 타입은 promise이다.  
띠라서 일반 함수에는 await을 사용할 수 없다.


```javascript
function gotCodestates(){
    return new Promise((resolve, reject) => {
        setTimeout(() => { resolve('1, go to codestates')}, 100)
    })
}

function sitAndCode(){
    return new Promise((resolve, reject) => {
        setTimeout(() => { resolve('2, sit and code')}, 100)
    })
}

function eatLunch(){
    return new Promise((resolve, reject) => {
        setTimeout(() => { resolve('3, eat lunch')}, 100)
    })
}

function goToBed(){
    return new Promise((resolve, reject) => {
        setTimeout(() => { resolve('4. gotoBed')}, 100)
    })
}

/*
gotoCodeState()
.then(data => {
    console.log(data)
    return sitAndCode()
})
.then(data => {
    console.log(data)
    return eatLunch()
})
.then(data => {
    console.log(data)
    return goToBed()
})
.then(data => {
    console.log(data)
})
*/

const result = async() => {
    // 마치 일반함수인것처럼 await을 추가해 순차적으로 사용하고 있다.
    const one = await gotoCodeStates();
    console.log(one);

    const two = await sitAndCode();
    console.log(two);

    const three = await eatLunch();
    console.log(three);

    const four = await goToBed();
    console.log(four);
}

reuslt();
```

## Timer API
- setTimeout(callback, millisecond)  

```javascript
/* setTimeout(callback, millisecond) 
    
    description : 
        일정 시간 이후에 함수를 실행하도록 한다.
    params : 
        callback : 실행할 callback 함수
        millisecond : callback 함수 실행 전 기다려야할 시간
    return :
        임의의 타이머 ID

*/

setTimeout(function(){
    console.log('1초 후 실행');
}, 1000);
```

- clearTimeout

- setInterval(callback, millisecond)  

```javascript
/* setInterval(callback, millisecond) 
    
    description : 
        일정 시간의 간격을 가지고 함수를 반복적으로 실행
    params : 
        callback : 실행할 callback 함수
        millisecond : 반복적으로 함수를 실행시키기 위한 시간 간격
    return :
        임의의 타이머 ID

*/

setInterval(function(){
    console.log('1초 마다 실행');
}, 1000);
```

- cleanInterval(timerID)  

```javascript
/* cleanInterval(timerID) 
    
    description : 
        반복 실행 중인 타이머를 종료한다.
    params : 
        timerID : 종료할 타이머 ID
    return :
        없음.

*/
const timer = setInterval(function(){
    console.log('1초마다 실행');
}, 1000);

// 더이상 반복되지 않음.
cleanInterval(timer);

```

## bind  

```javascript
bind(this, args);
    /*
    params :
        this : generated fuinction
                if undefined or null, `this` value of the return value becomes global.
        args : parameters that go to the original function
    returns : 
        function
    */
```

## Node js Modules
`Node.js`의 경우 많은 API가 비동기로 작성되어 있다.  
이는 `Node.js`의 정의에서부터 알 수 있다.  

> Node.js는 비동기 이벤트 기반 자바스크립트 런타임 입니다.  

### Module
건축으로부터 비롯된 용어로, 모듈이란 어떤 기능을 조립할 수 있는 형태로 만든 부분이다.  

### How to use Modules in Node.js
Node.js 내장 모둘 목록은 다음 [링크](https://nodejs.org/dist/latest-v14.x/docs/api/)에서 찾을 수 있다.  
이전에 다른 모듈을 사용하기 위해서는 `script`태그 안에서 호출했지만, `Node.js`안에서는 `require`구문을 사용한다.  

```javascript
// 파일 시스템 모듈을 불러오기
const fs = require('fs');

// DNS 모듈을 불러오기
const dns = require('dns');
```

### Third party module
built-in module이 아닌 써드 파티 모듈을 사용할 때에는 npm을 이용하여 설치한 후 사용한다.
```bash
npm install underscore
```
```javascript
const _ = require('underscore');
```

## Further Study
- AnimationAPI
- AJAX (XHR)
- Principle of Event Loop