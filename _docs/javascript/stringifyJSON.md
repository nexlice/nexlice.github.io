---
title: StringifyJSON
tags: 
 - JavaScript
 - JSON

description: Learn about the concepts of StringifyJSON!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

## Achievement Goals
- json 구조가 재귀 함수를 사용할 수 있는 Tree구조이다.
- JSON.stringify와 JSON.parse가 각각 serialize, deserailize에 대응한다.
- JSON.stringify와 JSON.parse를 사용하여 JavaScript값과 JSON을 넘나들 수 있다.
- JSON에 재귀 호출을 사용할 떄, 어디에 사용해야할 지 알 수 있다.

---

## JSON
`JSON` 은 JavaScript Object Notation의 아니셜로,  
데이터 교환을 위해 만들어진 객체 형태의 포맷이다.  
다음 객체를 전송한다고 해보자.  
```javascript
const message = {
    sender: "nexlice",
    receriver: "dk",
    message: "Stop sleeping!"
}
```

메세지 객체가 전송 가능하려면, 다음 조건 중 적어도 하나를 만족해야 한다.  
> 전송 가능한 조건 (transferable condition)
> - 수신자와 발신자가 같은 프로그램을 사용한다.
> - 문자열을 범용적으로 읽을 수 있어야 한다.  

객체는 타입 변환을 이용해 String으로 변환할 경우, 객체 내용을 포함하지 않는다.  
JavaScript에서 객체에 메서드 `message.toString()`이나,  
형변환 `String(message)`를 시도하면, `[object Object]` 결과를 리턴한다.  

이 문제를 해결하기 위해, 객체를 `JSON`의 형태로 변환하거나, `JSON`을 객체의 형태로 변환한다.  
- `JSON.stringify` : Object type을 JSON으로 변환한다.
- `JSON.parse`: JSON을 Object type으로 변환한다.  

```javascript
 let transferableMessage = JSON.stringify(message)
 console.log(transferableMEssage);
 console.log(typeof(transferableMessage));
```
```bash
`{"sender":'nexlice", "receriver":"dk", "message":"Stop sleeping!"}`
'string'
```
> 이렇게 stringify하는 과정을 직렬화(serialize)라고 한다.  

수신자는 객체를 직렬화한 문자열을 `JSON.parse`를 사용하여 다시 객체의 형태로 만들 수 있다.  
```javascript
let packet = `{"sender":'nexlice", "receriver":"dk", "message":"Stop sleeping!"}`

let obj = JSON.parse(packet)
console.log(obj);
console.log(typeof(obj));
```
```bash
{
    sender: "nexlice",
    receriver: "dk",
    message: "Stop sleeping!"
}

`object`

```

> 이렇게 `JSON.parse`를 적용하는 과정을 역직렬화(deeserialize)라고 한다.  

---

### Base rule of JSON
딕셔너리 객체와 JSON의 차이는 다음과 같다.  
||자바스크립트 객체|JSON|
|:---|:---:|:---:|
|키|키는 따옴표 없이 쓸 수 있다|반드시 큰 따옴표로 감싸야 함|
|문자열 값|어떤 형태의 따옴표도 사용 가능|반드시 큰 따옴표로 감싸야 함|

또한 JSON은 키와 값 사이, 그리고 키-값 쌍 사이에는 공백이 있어서는 안된다.  

---

## Further Study
- JavaScript recursion memory leak
- tail recursion in js
- js tower of hanoi in recursion
- js combinatio in recursion