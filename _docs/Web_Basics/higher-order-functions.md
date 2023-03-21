---
title: Higher Order Functions
tags: 
 - JavaScript
 - First Class Citizen
 - Hoisting
 - HTML
 - pipe
description: Learn about basic Higher Order Functions!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

# Higher Order Functions

## Achievement Goals
- 일급 객체 `first-class citizen`의 세가지 특징을 설명할 수 있다.  
- 고차함수(higher order function)에 대해 설명할 수 있다.  
- 고차함수를 `JavaScript`로 작성할 수 있다.  

---

## First Class Citizen
### 특별한 대우를 받는 함수
비행기의 First class와 economy class는 항공사로부터 다른 대우를 받는다.  
`JavaScript`에도 특별한 대우를 받는 `일급 객체` `first-class citizen`이 있다.  

대표적인 일급 객체 중 하나가 `함수`이다.  
`JavaScript`에서 함수는 아래와 같이 특별하게 취급된다.  
- 변수에 할당 (assignment) 할수 있다.
- 다른 함수의 인자 (argument)로 전달될 수 있다. 
- 다른 함수의 결과로서 리턴될 수 있다. 

함수를 변수에 할당할 수 있기 때문에, 함수를 배열의 요소나 객체의 속성값으로 저장할 수 있다.  
이는 함수를 데이터 (string, number, boolean, array, object)를 다루듯이 다룰 수 있다는 것을 의미한다.  

---

### Hoisting
위의 함수 표현식(`function expression`)은 함수 선언식(`fucntion declaration`)과 다르게 호이스팅 `Hoisting`이 적용되지 않는다.  
- 호이스팅은 선언된 위치에 관계없이 어디서든 함수를 사용할 수 있도록 한다.  
- 코드가 실행되는 과정에서 함수 선언부를 코드의 최상단으로 끌어올리는 것처럼 보이게 한다.  

`함수 선언식`의 `호이스팅`에 지나치게 의존하면, 코드의 유지 보수가 쉽지 않다.  
코드 리뷰나 디버깅을 할 떄, 코드를 위아래로 보지 않으면 해석이 어려워진다..  

`함수 선언식`은 어느 위치에나 선언할 수 있고, 함수의 **실행 위치**도 중요하지 않다.    
반면에, `함수 표현식`은 함수의 할당과 실행의 위치에 따라 결과가 달라지기 떄문에, 코드의 위치를 어느정도 예측할 수 있다.  
`호이스팅`을 제외하면, 함수 선언식과 함수 표현식은 크게 차이가 없다.  
다만, 함수 표현식의 경우는 함수 변수에 저장될 수 있다는 사실을 보다 분명하게 보여준다.  

그리고 함수는 변수에 저장된 데이터를 인자로 받거나, 리턴값으로 사용할 수 있다.  
함수도 변수에 저장될 수 있기 때문에, 함수를 인자로 받거나, 리턴 값으로 사용할 수 있다.  
    
---

## Definition
고차함수 (`higher order functions`)는 함수를 인자 (argument)로 받을 수 있고, 함수의 형태로 리턴할 수 있는 함수이다.  
함수는 변수에 저장할 수 있고, 함수를 담은 변수를 인자로 받을 수 있다.  
마찬가지로, 함수 내부에서 변수에 함수를 할당할 수 있다.  
그리고 함수는 이 변수를 리턴할 수 있다.  
여기서 변수에 할당하지 않고 함수를 바로 이용할 수 있다.  
어떤 고차 함수에 함수를 인자로 전달하고, 고차함수는 함수 자체를 리턴한다.  
변수가 빠져있을 뿐, 동일하게 동작한다.  
정리하자면, 함수는 객체처럼 다룰 수 있다.  
  
이때 다른 함수(caller)의 인자(argument)로 전달되는 함수를 콜백함수 (`callback function`) 이라고 한다.  
> 콜백함수의 이름은, 어떤 작업이 완료되었을 때 호출하는 경우가 많아서, 답신 전화를 뜻하는 콜백이라는 이름이 붙여졌다.  
  
콜백 함수를 전달받은 고차함수는, 함수 내부에서 이 콜백 함수를 호출(`invoke`)할 수 있다.  
caller는 조건에 따라 콜백 함수의 실행 여부를 결정할 수 있다.  
아예 호출하지 않을 수도 있고, 여러번 실행할 수도 있다.  

> '함수를 리턴하는 함수'는 모양새가 특이한 만큼, 부르는 용어가 따로 있다.  
> '함수를 리턴하는 함수'를 고안해 낸 논리학자 하스켈 커리(Haskell Curry)의 이름을 따, `커리함수`라고 한다.  
> 따로 커리 함수라는 용어를 사용하는 경우에는, 고차 함수란 용어를 '함수를 인자로 받는 함수'에만 한정해 사용하기도 한다.  
> 그러나 정확하게 구분하자면, 고차함수가 커리함수를 포함한다.  

---

1. 변수에 함수를 할당하는 경우
``` javascript
/*
 * 아래는 변수 square에 함수를 할당하는 함수 표현식 입니다.
 * 자바스크립트에서 함수는 일급 객체에기 때문에 변수에 저장할 수 있습니다.
 * 
 * 함수 표현식은 할당 전에 시용할 수 없습니다.
 * sqaure(7); // --> ReferenceError: Can't find variable: square
*/

const sqaure  = function (num) {
    return num * num;
};

// square에는 함수가 저장되어 있으므로 (일급 객체), 함수 호출 연산자 '()'를 사용할 수 있습니다.
output = square(7);
console.log(output); // -->49
```

---

1.  다른 함수를 인자로 받는 경우  

```javascript
function double(num) {
    return num * 2;
}

function doubleNum(func, num) {
    return func(num)
}

/*
 * 함수 doubleNum은 다른 함수를 인자로 받는 고차함수입니다.
 * 함수 doubleNum의 첫 번째 인자 func에 함수가 들어올 경우
 * 함수 func는 함수 doubleNum의 콜백 함수 입니다.
 * 아래와 같은 경우, 함수 double 은 함수 doubleNum의 콜백 함수입니다.
*/
let output = doubleNum(double, 5);
console.log(output); // --> 8
```

---


1. 함수를 리턴하는 경우  

```javascript
function adder(added) {
    return function (num) {
        return num + added
    };
}

/*
 * 함수 adder는 다른 함수를 리턴하는 고차 함수 입니다.
 * adder는 인자 한 개를 입력받아수 함수(익명 함수)를 리턴합니다.
 * 리턴되는 익명 함수는 인자 한 개를 받아서 adder와 더한 값을 리턴합니다.
 */

// adder(5)는 함수이므로 함수 호출 연산자 '()'를 사용할 수 잇습니다.
let output = adder(5)(3); // --> 8
console.log(output); // --> 8

// adder가 리턴하는 함수를 변수에 저장할 수 있습니다.
// javascript에서 함수는 일급 객체이기 떄문입니다.
const add3 = adder(3);
output = add3(2);
console.log(output); // --> 5
```

---

1. 함수를 인자로 받고, 함수를 리턴하는 경우  

```javascript
functino double(num){
    return num * 2;
}

function doubleAdder(added, func){
    const doubled = func(added);
    return function (num) {
        return num + doubled;
    };
}

/*
 * 함수 doubleAdder는 고차 함수입니다.
 * 함수 doubleAdder의 인자 func는 함수 doubleAdder의 콜백 함수입니다.
 * 함수 double은 함수 doubleAdder의 콜백으로 전달되었습니다.
*/

// doubleAdder(5, double)는 함수이므로 함수 호출 기호 '()'를 사용할 수 있습니다.
doubleAdder(5, double)(3); // -->13

//doubleAdder가 리턴하는 함수를 변수에 저장할 수 있습니다. (일급 객체)
const addTwice3 = doubleAdder(3, double);
addTwice3(2); // --> 8
```

---

## Practice

### Decorator like
```javascript
function pipe(...args) {
    // TODO: 여기에 코드를 작성합니다.
    return function(num){    
        let output = num;
        // console.log(args);
        for (let i = 0; i < args.length; i++) {
            output = args[i](output);
        }
        return output
   };
}
  

function square(num) {
    return num * num;
}

function add5(num) {
    return num + 5;
}

function mul3(num) {
    return num * 3;
}

function isOdd(num) {
    return num % 2 !== 0;
}

let output = pipe(add5, square);
console.log(output(4)); // --> 81

output = pipe(square, add5, mul3);
console.log(output(4)); // --> 63

output = pipe(square, mul3, add5, add5, isOdd);
console.log(output(4)); // --> false
```

---

### Split with specific character

```javascript
function callbackOnly(callback, response) {
    // TODO: 여기에 코드를 작성합니다.
    if (response['status'] === 'fail'){
        return 'Something went wrong!'
    }
    else if(response['status'] === 'success'){
        return callback(response['data'])
    }
  
}
  

function getDomain(email) {
    return email.split('@')[1].split('.')[0];
}
  
function getUserId(email) {
    return email.split('@')[0];
}
  
let output = callbackOnly(getDomain, {
    status: 'success',
    data: 'mike@codestates.com',
});
console.log(output); // --> codestate
  
output = callbackOnly(getUserId, {
    status: 'success',
    data: 'mike@codestates.com',
});
console.log(output); // --> mike
  
output = callbackOnly(getUserId, {
    status: 'fail',
    data: 'mike@codestates.com',
  });
console.log(output); // --> 'Something went wrong!'
```

---

### Simple map
```javascript
function mapCallback(func, arr) {
    // TODO: 여기에 코드를 작성합니다.
    let output = arr
    for(let i = 0; i < arr.length; i++){
        output[i] = func(arr[i])
    }
    return output;
  }

  
  function square(num) {
    return Math.pow(num, 2);
  }
  
  function mul10(num) {
    return num * 10;
  }
  
  let output = mapCallback(square, [2, 4, 7]);
  console.log(output); // --> [4, 16, 49]
  
  output = mapCallback(mul10, [2, 4, 7]);
  console.log(output); // --> [20, 40, 70]
  
  output = mapCallback(square, []);
  console.log(output); // --> []
```

---

### push, unshift, splice, pop, shift

```javascript
// https://gent.tistory.com/295

function filterCallback(func, arr) {
  // TODO: 여기에 코드를 작성합니다.
  let output = []
  for(let i = 0; i < arr.length; i++){
      if (func(arr[i])){
        output.push(arr[i])
      }
  }
  return output;
}

function isOdd(num) {
  return num % 2 === 1;
}

function isEven(num) {
  return !isOdd(num);
}

let output = filterCallback(isOdd, [1, 2, 3, 4]);
console.log(output); // --> [1, 3]

output = filterCallback(isEven, [1, 2, 3, 4]);
console.log(output); // --> [2, 4]
```

---

## Further Studies
- map vs reduce
- currying vs closure
- declarative programming vs imperative programming
- function composition in JavaScript