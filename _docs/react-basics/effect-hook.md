---
title: Effect Hook
tags: 
 - react
 - Pure Function
 - Side Effect
 - useEffect

description: Learn about the concepts of Effect Hook!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

{% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %}

## Side Effect
우리말로는 **부수 효과**라 한다.  
함수 내에서 어떤 구현이 함수 외부에 영향을 끼치는 경우, 해당 함수는 `Side Effect`가 있다 말한다.  

```javascript
  // bar 함수는 함수 외부 변수인 foo를 변경시키므로 Side Effect를 발생시킨다. 
let foo = 'hello';

function bar(){
  foo = 'world'
}

bar();
```

--- 

## Pure Function
`순수 함수`란, 오직 함수의 입력만이 함수의 결과에 영향을 주는 함수를 의미한다.  
함수의 입력이 아닌 다른 값이 함수의 결과에 영향을 미치는 경우, `순수 함수`라 부를 수 없다.  
또한 `순수 함수`는, 입력으로 전달된 값을 수정하지 않는다.  

```javascript
function upper(str) {
  // toUpperCase 메서드는 원본을 수정하지 않는다. (Immutable)
  return str.toUpperCase();
}

upper('hello'); //'HELLO
```

---

## Function Component
리액트의 함수 컴포넌트는, `props`가 입력으로, `JSX Element`가 출력으로 나간다.  
여기에는 그 어떤 `Side Effect`도 없으며, 순수 함수로 작동한다.  
```javascript
function SingleTweet({writer, body, createdAt}) {
  return <div>
    <div>{writer}</div>
    <div>{createdAt}</div>
    <div>{body}</div>
  </div>
}
```

하지만 보통 React 어플리케이션을 작성할 때에는, `AJAX` 요청이 필요하거나, LocalStorage 또는 타이머와 같은,  
`React와 상관없는 API`를 사용하는 경우가 발생할 수 있다.  
**이는 React의 입장에서는 전부 Side Effect이다.**  
React는 Side Effect를 다루기 위한 Hook인 `Effect Hook`을 제공한다.  

---

## useEffect
`useEffect`는 컴포넌트 내에서 `Side Effect`를 실행할 수 있게하는 `Hook`이다.  
다음 컴포넌트에서 실행하는 Side Effect는 브라우저 API를 사용하여, 타이틀을 변경하는 것이다.  

```javascript
import { useEffect, useState } from "react";
import "./styles.css";

export default function App() {
  const proverbs = [
    "좌절감으로 배움을 늦추지 마라",
    "Stay hungry, Stay foolish",
    "Memento Mori",
    "Carpe diem",
    "배움에는 끝이 없다"
  ];
  const [idx, setIdx] = useState(0);

  const handleClick = () => {
    setIdx(idx === proverbs.length - 1 ? 0 : idx + 1);
  };

  return (
    <div className="App">
      <button onClick={handleClick}>명언 제조</button>
      <Proverb saying={proverbs[idx]} />
    </div>
  );
}

function Proverb({ saying }) {
  useEffect(() => {
    document.title = saying;
  });
  return (
    <div>
      <h3>오늘의 명언</h3>
      <div>{saying}</div>
    </div>
  );
}
```

`useEffect(함수)`  
`useEffect`의 첫번째 인자는 함수이다. 해당 함수 내에서 side effect를 실행한다.  
이 함수는 다음과 같은 조건에서 실행된다.  
![side effect 실행](/assets/img/side-effect-execution.png)  

- 컴포넌트 생성 후 처음 화면에 렌더링
- 컴포넌트에 새로운 props가 전달되며 렌더링
- 컴포넌트에 상태(state)가 바뀌며 렌더링

이와 같이 매 번 새롭게 컴포넌트가 **렌더링**될 떄 Effect Hook이 실행된다.  

---

### Precautions
Hook을 쓸 때 주의점은 다음 두가지 정도 있다.  

- 최상위에서만 Hook을 호출한다.
- React 함수 내에서 Hook을 호출한다.  

자세한 내용은 [공식문서](https://ko.reactjs.org/docs/hooks-rules.html#only-call-hooks-at-the-top-level)를 참조하자.  

---

## Dependency array
`useEffect`의 두 번째 인자는 배열이다. 
이 배열은 조건을 담고 있다.  
여기서 조건은 `boolean` 형태의 표현식이 아닌, **어떤 값의 변경이 일어날 때**를 의미한다.  
따라서, 해당 배열엔 **어떤 값**의 목록이 들어간다.  
이 배열을 특별히 종속성 배열이라 부른다.  

다음 예제에는 3가지 상태가 존재한다.  
- proverbs
- effect : 필터링할 문자열
- count

이 예제는, `filter`가 변할 때에만, effect 함수가 실행된다.  
한편, 카운트를 올리는 버튼은 컴포넌의 상태가 바뀌고 업데이트 되지만, effect 함수는 실행되지 않는다.  
이는 종속성 배열에는 `filter`만 존재하고, `count`는 존재하지 않기 때문이다.  

```javascript
import { useEffect, useState } from "react";
import "./styles.css";
import { getProverbs } from "./storageUtil";

export default function App() {
  const [proverbs, setProverbs] = useState([]);
  const [filter, setFilter] = useState("");
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("언제 effect 함수가 불릴까요?");
    const result = getProverbs(filter);
    setProverbs(result);
  }, [filter]);

  const handleChange = (e) => {
    setFilter(e.target.value);
  };

  const handleCounterClick = () => {
    setCount(count + 1);
  };

  return (
    <div className="App">
      필터
      <input type="text" value={filter} onChange={handleChange} />
      <ul>
        {proverbs.map((prvb, i) => (
          <Proverb saying={prvb} key={i} />
        ))}
      </ul>
      <button onClick={handleCounterClick}>카운터 값: {count}</button>
    </div>
  );
}

function Proverb({ saying }) {
  return <li>{saying}</li>;
}

```

`useEffect(함수, [종속성1, 종속성2, ...])`  
`useEffect`의 두 번쨰 인자는 종속성 배열이다.  
배열 내의 종속성 값이 변할 떄, 첫 번째 인자의 함수가 실행된다.  
배열 내의 어떤 값이 변할 때에만, (effect가 발생하는)함수가 실행된다.  

---

### 단 한번만 실행되는 Effect 함수
useEffect의 두가지 형태에 대해서 알아보았다.  
이 떄 두번째 인자에 빈 배열을 넣는것과 인자에 함수만 넣는 것의 차이는 무엇일까?  

1. `useEffect(함수, [])`
2. `useEffect(함수)`  

2번 형태의 useEffect는 컴포넌트가 처음 생성되거나, props가 업데이트 되거나, 상태(state)가 업데이트 될 떄, effect 함수가 실행된다.  
반면, 1번 처럼 빈 배열을 두 번쨰 인자로 사용하면, 이 때에는 **컴포넌트가 처음 생성될 때에만** effect 함수가 실행된다.  
외부 API를 통해 리소스를 받고 더이상 API 호출이 필요하지 않을 때 활용할 수 있다.  

---

## Examples
앞선 예제(Data Fetching)를 통해 개념을 이해해보자.  
목록 내 필터링을 구현하기 위해서는 다음과 같은 두가지 접근이 있을 수 있다.  
1. **컴포넌트 내에서 필터링** : 전체 목록 데이터를 불러오고, 목록을 검색어로 filter하는 방법.  
2. **컴포넌트 외부에서 필터링** : 컴포넌트 외부로 API 요청을 할 떄, 필터링한 결과를 받아오는 방법.  
(보통 서버에 매번 검색어와 함꼐 요청하는 경우가 이에 해당한다.)

---

### 컴포넌트 내에서 필터링
처음 단 한번, 외부 API로부터 명언 목록을 받아오고, `filter` 함수를 이용한다.  
```javascript
import { useEffect, useState } from "react";
import "./styles.css";
import { getProverbs } from "./storageUtil";

export default function App() {
  const [proverbs, setProverbs] = useState([]);
  const [filter, setFilter] = useState("");

  useEffect(() => {
    console.log("언제 effect 함수가 불릴까요?");
    const result = getProverbs();
    setProverbs(result);
  }, []);

  const handleChange = (e) => {
    setFilter(e.target.value);
  };

  return (
    <div className="App">
      필터
      <input type="text" value={filter} onChange={handleChange} />
      <ul>
        {proverbs
          .filter((prvb) => {
            return prvb.toLowerCase().includes(filter.toLowerCase());
          })
          .map((prvb, i) => (
            <Proverb saying={prvb} key={i} />
          ))}
      </ul>
    </div>
  );
}

function Proverb({ saying }) {
  return <li>{saying}</li>;
}
```

---

### 컴포넌트 외부에서 필터링
앞서 Dependency array에서 보았던 코드와 동일하다.  
```javascript
import { useEffect, useState } from "react";
import "./styles.css";
import { getProverbs } from "./storageUtil";

export default function App() {
  const [proverbs, setProverbs] = useState([]);
  const [filter, setFilter] = useState("");
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("언제 effect 함수가 불릴까요?");
    const result = getProverbs(filter);
    setProverbs(result);
  }, [filter]);

  const handleChange = (e) => {
    setFilter(e.target.value);
  };

  const handleCounterClick = () => {
    setCount(count + 1);
  };

  return (
    <div className="App">
      필터
      <input type="text" value={filter} onChange={handleChange} />
      <ul>
        {proverbs.map((prvb, i) => (
          <Proverb saying={prvb} key={i} />
        ))}
      </ul>
      <button onClick={handleCounterClick}>카운터 값: {count}</button>
    </div>
  );
}

function Proverb({ saying }) {
  return <li>{saying}</li>;
}
```

---

#### 두 방식의 차이점
외부 API를 지금은 직접 구현했지만, 이는 **서버 요청**으로 대체할 수 있다.  
||장점|단점|
|:---:|:---:|:---:|
|컴포넌트 내부에서 처리|HTTP 요청의 빈도를 줄일 수 있다|브라우저(클라이언트)의 메모리 상에 많은 데이터를 갖게 되므로, 클라이언트의 부담이 늘어난다.|
|컴포넌트 외부에서 처리|클라이언트가 필터링 구현을 생각하지 않아도 된다|빈번한 HTTP 요청이 일어나며, 서버가 필터링을 처리하므로 서버가 부담을 가져간다|

---

### AJAX
fetch API를 사용하면 다음과 같아진다.  
```javascript
useEffect(() => {
  fetch(`http://서버주소/proverbs?1=${filter}`)
    .then(resp => resp.json())
    .then(result => {
      setProverbs(result);
    });
}, [filter]);
```

---

### Loading Indicator
네트워크 요청이 즉각적인 응답을 항상 가져다 주는 것은 아니기에,  
외부 API 접속이 느릴 경우를 고려하여, 로딩 화면(loading indicator)를 구현해야한다.  
**state**와 함께 구현해보자.  

```javascript
const [isLoading, setIsLoading] = useState(true);

// LoadingIndicator 컴포넌트는 이미 구현했다고 가정한다.  
return {isLoading? <LoadingIndicator /> : <div>로딩 완료 화면></div>}
```

fetch 요청의 전후로 `setIsLoading`을 설정해주어 더 나은 UX를 구현할 수 있다.  
```javascript
useEffect(() => {
  setIsLoading(true);%
    fetch(`http://서버주소/proverbs?1=${filter}`)
    .then(resp => resp.json())
    .then(result => {
      setProverbs(result);
      setIsLoading(false);
    });
}, [filter]);
```

---

### Further Study
실무에서는 서버의 부담과 클라이언트의 부담이 적절하게 분배된 어플리케이션 구조를 가지게 된다.  

**클라이언트가 서버에 요청을 덜 보내는 방법**  
 - [Throttle a series of fetch requests in JavaScript](https://dev.to/edefritz/throttle-a-series-of-fetch-requests-in-javascript-ka9)
 - [throttle vs debounce](https://webclub.tistory.com/607)

**서버가 클라이언트에게 돌려줄 응답을 캐싱하는 방법**  
HTTP 및 서버 구현에 대한 이해가 필요하다.  
 - [HTTP caching](https://developer.mozilla.org/ko/docs/Web/HTTP/Caching)
