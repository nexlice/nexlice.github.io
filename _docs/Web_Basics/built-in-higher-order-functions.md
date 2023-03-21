

# Built in higher order functions in JavaScript
## achievement goals
- 배열 내장 고차함수 filter에 대해서 이해할 수 있다.
- filter에 대한 이해를 기반으로, 나머지 고차함수를 스스로 학습할 수 있다.
    - forEach, find, filter, map, reduce, sor, some, every
- 추상화(abstraction)에 대해서 설명할 수 있다.
- 추상화의 관점에서 고차 함수가 갖는 이점에 대해서 설명할 수 있다.
- 고차 할수를 활용하여 프로그램을 작성할 수 있다.


## filter
배열의 filter 메서드는 모든 배열의 요소 중에서 특정 조건을 만족하는 요소를 걸러내는 메소드이다.  
예를들어 배열에서 짝수만을 걸러내거나, 18보다 작은 수만을 걸러낼 수 있다.  
string타입을 요소로 갖는 배열에서, 길이가 10 이하인 문자열만 걸러내거나, 'korea'만 걸러낼 수도 있다.  

여기서 걸러내는 기준이 되는 특정 조건은 filter 메서드의 인자로 전달된다.  
이때 전달되는 조건은 함수의 형태이다.  
filter메서드는 걸러내기 위한 조건을 명시한 함수를 인자로 받기 때문에 고차함수이다.  
filter메서드가 동작하는 방식은 다음과 같다. 

```javascript
// 아래 코드에서 '짝수'와 '길이 5 이하'는 문법 오류(syntax error)에 해당한다.
let arr = [1, 2, 3];
arr.filter = function (arr, func) {
    const newArr = [];
    for (let i = 0; i < arr.length; i++){
        if (func(arr[i]) === true) {
            newArr.push(this[i]);
        }
    }
    return newArr;
};

// 보다 정확한 정의는 프로토 타입과 this를 통해 이해해야한다.
Array.prototype.filter = function(func) {
    const arr = this;
    const newArr = []
    for (let i = 0; i < arr.length; i++) {
        if (func(arr[i]) === true) {
            newArr.push(this[i])
        }
    }
    return newArr;
}
```

filter 메서드는 배열의 요소를, 인자를 전달되는 콜백 함수에 다시 전달한다.  
콜백 함수는 전달받은 배열의 요소를 받아 함수를 실행하고, 콜백 함수 내부의 조건에 따라 true, false를 리턴해야한다.  
적어도 filter 메서드는 이런 함수를 기대하고 있다.  
최종 코드는 다음과 같다.
```javascript
const isEven = function (num) {
    return num % 2 === 0;
}

let arr = [1, 2, 3, 4];

let output = arr.filter(isEven);
console.log(output); // --> [2, 4]

const isLteFive = function (str) {
    // Lte = less then equal
    return str.length <= 5;
}

arr = ['hello', 'code', 'happy', 'hacking'];
let output = arr.filter(isLteFive);
console.log(output); // --> ['hello', ' code' , 'happy']
```

### 추가적으로 학습할 것들
filter 메서드에 들어가는 콜백 함수는 truthy 또는 falsy를 리턴할 수 있다.  
그러나 filter 메서드에 들어가는 콜백 함수는 Deep equality를 통해 조건을 명확하게 밝히는 것을 권장한다.  

## 요약
map : 배열을 반환한다. 
reduce: 값을 반환한다.
filter: 조건을 적용한 배열을 반환한다.
reduce안에서 조건문을 해도 괜찮지만 관심사 분리를 통해 분리하는게 좋다. 아마도?  

## map
map은 모든 요소들에 대해서 동일한 행동을 한 결과를 반환한다.
행동은 직접 작성해야하며, 함수로 작성해야한다.  
또한 기존 배열을 수정하지 않는다.  

```javascript
const cartoons = [
    {
        id 1,
        bookType: 'cartoon',
        title: '식객',
        subtitle: '어머니의 쌀',
        createAt: '2003-09-09',
        genre: '요리',
        artist: '허영만',
        averageScore: 9.66,
    },
    {
        id: 2,
        // .. 이하 생략
    },
    // .. 이하 생략
]; // 만화책의 모음

const findSubtitle = function(cartoon){
    // 한 요소에 대한 행동을 정의한다.
    return cartoon.subtitle;
}; // 만화책 한 권의 제목을 리턴하는 로직(함수)

const subtitles = cartoons.map(findSubtitle); // 각 책의 부제 모음
```

## filter
```javascript
const cartoons = [
    {
        id 1,
        bookType: 'cartoon',
        title: '식객',
        subtitle: '어머니의 쌀',
        createAt: '2003-09-09',
        genre: '요리',
        artist: '허영만',
        averageScore: 9.66,
    },
    {
        id: 2,
        // .. 이하 생략
    },
    // .. 이하 생략
]; // 만화책의 모음

const isCreatedAt2003 = function(cartoon){
    // 조건을 구현한다.
    const fullYear = new Date(cartoon.createAt).getFullYear()
    return fullYear === 2003;
}; // 단행본 한 권의 출판년도가 2003인지 확인하는 함수

const filteredCartoons = cartoons.filter(isCraetedAt2003); // 출판년도가 2004년인 책의 모음
```

## Reduce
여러 데이터를 하나의 데이터로 응축(reduce) 할 때 사용한다.
```javascript
const cartoons = [
    {
        id 1,
        bookType: 'cartoon',
        title: '식객',
        subtitle: '어머니의 쌀',
        createAt: '2003-09-09',
        genre: '요리',
        artist: '허영만',
        averageScore: 9.66,
    },
    {
        id: 2,
        // .. 이하 생략
    },
    // .. 이하 생략
]; // 만화책의 모음

const scoreReducer = function(sum, cartoon){
    return sum + cartoon.averageScore;
}; // 단행본 한 권의 평점을 누적값에 더한다.

let initialValue = 0; // 숫자 형태로 평점을 누적한다.
const cartoonAvgScore = cartoons.reduce(scoreReducer, initialValue) / cartoons.length;
// 모든 책의 평점을 누적한 평균을 구한다.
```

reduce는 더욱 다양한 방법으로 활용할 수 있다.  

### 배열을 문자열로

```javascript
function joinName(resultStr, user) {
    resutlStr = resultStr + user.name ', ';
    return resultStr;
}

let users = [
    {name: 'Tim', age: 40}.
    {name: 'Satya', age: 30}.
    {name: 'Sundar', age: 50}
];

users.reduce(joinName, '');
```
콜백 함수 joinName은 users 배열 안에 있는 요소의 이름을 하나로 응축한다.  

### 배열을 객체로

```javascript
function makeAddressBook(addressBook, user) {
    let firstLetter = user.name[0];

    if (firstLetter in addressBook) {
        addressBook[firstLetter].push(user);
    } else {
        addressBook[firstLetter] =[];
        addressBook[firstLetter].push(user);
    }

    return addressBook;
}

let users = [
    {name: 'Tim', age: 40}.
    {name: 'Satya', age: 30}.
    {name: 'Sundar', age: 50}
];

users.reduce(makeAdressBook, {});
```

최종 리턴 값
```javascript
{
    T: [
        { name: 'Tim', age: 40 }
    ],
    S: [
        { name: 'Satya', age: 30 },
        { name: 'Sundar', age: 50 }
    ]
}
```


# 왜 꼭 고차함수여야 할까? Why higher order function?
## 높은 수준에서 생각하기
추상화때문이다.  
추상화는 복잡한 어떤 것을 압축해서 핵심만 추출한 상태로 만드는 것이 추상화이다.  

우리는 브라우저에서 주소를 입력했을 때 어떤 일이 정확하게 일어나는지 알지 못한다.  
일상 생활에서는 몰라도 되기 때문이다.  

마찬가지로 자바스크립트를 비롯한 많은 프로그래밍 언어 역시, 추상화의 결과이다.  
컴퓨터를 구성하는 장치인 CPU는 0과 1만 이해한다.  
크롬 개발자 도구의 콘솔 탭에서 어떤 과정을 거치는지 몰라도 우리는 잘 사용하고 있다.  
크롬의 자바스크립트 해석기(엔진)이 대신해주기 때문이다.  

추상화는 생산성의 향상을 부른다.  
- 함수 = 값을 전달받아 값을 리턴한다 = 값에 대한 복잡한 로직은 감추어져 있다 = 값 수준에서의 추상화

고차함수는 이 추상화의 수준을 사고의 추상화 수준으로 끌어올린다. 
- 값 수준의 추상화 : 단순히 값(value)을 전달받아 처리하는 수준
- 사고의 추상화 : 함수(사고의 묶음)를 전달받아 처리하는 수준

즉, 고차함수를 통해, 보다 높은 수준 (higher order)에서 생각할 수 있다.
- 고차함수 = 함수를 전달받거나 ㅎ마수를 리턴한다 = 사고(함수)에 대한 복잡한 로직은 감추어져 있다 = 사고 수준에서의 추상화
추상화 수준이 높아지는 만큼, 생산성도 비약적으로 상승한다.  
이를테면 배열 내장 함수인 unshift는 고차함수가 아니다.  
함수를 인자로 받아서 행동을 하지 않기 때문이다.  

## 일반적인, generic한 함수로 구성하기
다음과 같은 데이터가 있다고 하자.
```javascript
const data = [
    {
        gender: 'male',
        age: 24
    },
    {
        gender: 'male',
        age: 25
    },
    {
        gender: 'female',
        age: 27
    },
    {
        gender: 'female',
        age: 22
    },
    {
        gender: 'male',
        age: 29
    }
];
```

함수를 만들때 가능하면 매개변수화 (parameterization)을 하여 일반적으로 함수로 변경하는 것이 좋다.  
아래의 compose함수는 입력받은 함수를 순서대로 결합하는 고차함수이다.  
각각의 작업을 분리하여 compose의 인자로 전달되는 콜백 함수로 구성해보자.  

```javascript
function getOnlyMales(data) {
    return data.filter(function (d) {
        return d.gender ==='male';
    });
}

function getOnlyAges(data) {
    return data.map(function (d) {
        return d.age;
    });
}

function getAverage(data) {
    const sum = data.reduce(finction (acc, cur){
        return acc + cur;
    }, 0);
    return sum / data.length;
}

function compose(...funcArgs) {
    return function (data) {
        let result = data;
        for (let i = 0; i < funcArgs.length; i++) {
            result = funcArgs[i](result);
        }
        return result;
    };
}

const getAberageAgeOfMale = compose(
    getOnlyMales,
    getOnlyAges,
    getAverage
);

const result = getAverageAgeOfMale(data);
console.log(result); // --> 26

```

## underbar
이전에는 배열 메서드가 브라우저에서 자체적으로 지원되지 않던 시절이 있었다.  
그래서 선배 개발자들은 보다 나은 방법으로 배열이나 객체를 다루기 위한 라이브러리,  
즉 배열이나 객체를 다루기 위한 도구 모음집을 만들었다.  
배열, 객체를 다루는 라이브러리 Underbar에 대해서 알아보자.  

## 메서드
객체에 들어있는 함수를 의미한다.  
메서드는 dot notation과 bracket notation으로 접근한다.  
arr.map
arr["map"]

## map
arr.map(el, idx) 모양이다.  
여기서 idx는 옵션이다.  
map 함수는 원본에 영향을 주지 않는다.  
그래서 변수에 저장해서 써야한다.  

## filter
filter도 index를 사용 가능하다.

## reduce
하나로 응축시킨 값을 만들고 싶을 때 사용한다.  
요소를 한번씩 순회한다.  
어떤 값을 만드려고하는 것이기 때문에 초깃값이 필요하다.  
초깃값이 없다면 acc가 0번째 인덱스 요소를 갖게된다.  

초깃값을 설정했다면 초깃값이 첫 acc값이 된다.
reduce도 원본 배열에 영향을 주지 않는다.  

## 내장 메서드들
- forEach : for 와 같음
- find : 콜백 함수를 만족하는 요소를 반환한다.
- sort : 정렬. 
- some : 콜백함수를 만족하는 요소가 하나라도 있으면 true
- every : 콜백함수를 만족하지 않는 요소가 하나라도 있으면 있으면 false