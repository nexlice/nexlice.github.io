---
title: State & Props
tags: 
 - React
 - State
 - Props
 - Dataflow
 - Controlled Component

description: Learn about the concept of State and Props!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

{% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %}

# React State & Props
## Achievement Goals
- State, Props의 개념에 대해서 이해하고, 실제 프로젝트에 바르게 적용할 수 있다.  
- React 함수 컴포넌트(React Function Component)에서 State hook을 이용하여 State를 정의할 수 있다.  
- React 컴포넌트 (React Component)에 props를 전달할 수 있다.  
- 이벤트 핸들러 함수를 만들고 React에서 이용할 수 있다.  
- 실제 웹 애플리케이션의 컴포넌트를 보고 어떤 데이터가 State이고 Props에 적합한지 판단할 수 있다.  
- 실제 웹 애플리케이션 개발 시 State와 Props의 위치를 스스로 정할 수 있다.  
- React의 단방향 데이터흐름 (One-way data flow)에 대해 자신의 언어로 설명할 수 있다.  

## Props
**컴포넌트의 속성(property)을 의미한다.**  
이름, 성별과 같이 변하지 않는 외부로부터 전달받은 값으로, 웹 어플리케이션에서 해당 컴포넌트가 가진 속성에 해당한다.  

**부모 컴포넌트(상위 컴포넌트)로부터 전달받은 값이다.**  
React 컴포넌트는 javaScript 함수와 클래스로, props를 함수의 전달인다(arguments)처럼 전달 받아,  
이를 기반으로 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다.  
다라서, 컴포넌트가 최초 렌더링 될 때에 화면에 출력하고자하는 데이터를 담은, 초기값으로 사용할 수 있다.  

**객체 형태이다.**  
props로 어떤 타입의 값도 넣어 전달할 수 있도록 props는 객체의 형태를 가진다.  

**읽기 전용이다.**  
props는 외부로부터 전달받아 변하지 않는 값이다.  
그래서 props는 함부로 변경될 수 없는 읽기 전용(read-only) 객체이다.  

> 읽기 전용 객체가 아니라면 props를 전달받은 하위 컴포넌트 내에서 porps를 직접 수정 시,  
> props를 전달한 상위 컴포넌트의 값에 영향을 미칠 수 있게 된다.  
> 즉, 개발자가 의도하지 않은 side effect가 생기게 되고,  
> 이는 React의 하향식 데이터 흐름 원칙에 위배한다.  

###  How to use props
props를 사용하는 방법은 아래 3단계로 이루어진다.  
1. 하위 컴포넌트에 전달하고자하는 값(data)과 속성을 정의한다.
2. props를 이용하여 정의된 값과 속성을 전달한다.  
3. 전달받은 props를 렌더링한다.  

React에서 속성 및 값은 다음처럼 할당한다.  

```javascript
<Child attribute = { value } />
```


다음과 같은 상황이 있다고하자.  
``` javascript
function Parent() {
    return (
        <div className = "parent">
            <h1>I'm the parent</h1>
            <Child text = {"I'm child"}/>
        </div>
    );
};

function Child(props) {
    return (
        <div className = "child">
            <p>{props.text}</p>
        </div>
    );
};
```

Parent, Child 컴포넌트를 선언하고, Parent 컴포넌트가 Child 컴포넌트를 호출하는 구조이다.  
함수에 인자를 전달하듯이 React 컴포넌트에 props를 전달하고, 이 props가 필요한 모든 데이터를 갖고있다.  
  
props 렌더링은 JSX 안에 직접 불러서 사용하면 된다.  
다만 props는 객체이기 때문에, 이 객체의 `{key : value}` 는 Parent 컴포넌트에서 정의한 `{attrivute : value}` 의 형태를 띤다.  
다라서 JavaScript에서 객체의 value에 접근할 때 dot notation을 사용하는 것과 동일하게,  
props의 value 또한 dot notation으로 접근할 수 있다.  


``` javascript
function Parent() {
    return (
        <div className = "parent">
            <h1>I'm the parent</h1>
            <Child>"I'm child<Child/>
        </div>
    );
};

function Child(props) {
    return (
        <div className = "child">
            <p>{props.children}</p>
        </div>
    );
};
```
위처럼 값을 태그 사이의 value를 넣어 전달할 수 있다.  
이 경우, props.children를 이용하면 해당 value에 접근하여 사용가 능하다.  

```javascript
import "./styles.css";

const App = () => {
  const itemOne = "React를";
  const itemTwo = "배우고 있습니다.";

  return (
    <div className="App">
      <Learn text1={itemOne} text2={itemTwo} />
    </div>
  );
};

const Learn = (props) => {
  return (
    <div className="Learn">
      <p>
        {props.text1} {props.text2}
      </p>
    </div>
  );
};

export default App;
```
만약 여러개의 props를 전달하고 싶다면 whitespace로 구분하여 전달한다.  

## State
Toggle Switch나,  Counter처럼 컴포넌트 내부에서 변할 수 있는 값이다.  
State로 사용할 수 있는 **상태**의 종류는 다음과 같다.  

- 나이, 현재 사는 곳, 취업 여부, 결혼/연애 여부, 토글, 체크박스 


아래는 State를 사용한 간단한 예시이다.
```javascript
import React, { useState } from "react";
import "./styles.css";

function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };
  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={handleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}

export default CheckboxExample;
```

### useState
React에서는 state를 다루는 바법 중 하나로 useState 함수를 제공한다.  
useState 자체는 state hook이라 부른다.  
체크박스로 예시를 들어 useState를 쓰는 과정은 다음과 같다.  

- React로부터 useState를 불러온다.
```javascript
import { useState } from 'react';
```

- 이후 useState를 컴포넌트 안에서 호출한다.  
useState를 호출한다는 것은 "state"라는 변수를 선언하는것과 같으며,  
이 변수의 이름은 아무 이름으로 지어도 된다.  
일반적인 함수는 함수가 끝날 때 사라지지만, state 변수는 React에 의해 함수가 끝나도 사라지지 않는다.  
```javascript
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

    // 위의 코드는 아래와 같다.
    const stateHookArray = useState(false);
    const isChecked = stateHookArray[0];
    const setIsChecked = stateHookArray[1];
}
```
구조적으로 isChecked, setIsChecked는 useState의 리턴값을 구조 분해 할당한 변수이다.  

- useState를 호출하면 배열을 반환하는데, 배열의 0번째 요소는 **현재 state**변수이고,  
1번째 요소는 **이 변수를 갱신할 수 있는 함수**이다.  
useState의 인자로 넘겨주는 값은 **state의 초기값**이다.  

```javascript
const [state 저장 변수, state 갱신 함수] = useState(상태 초기 값);
```

### update state
- state를 갱신하려면 state 변수를 갱신할 수 있는 함수인, ```setIsChecked```를 호출한다.  
- 위의 예시의 경우, ```input[type=checkbox]``` JSX 엘리먼트의 값 변경에 다라서 ```isChecked```가 변경되어야 한다.  
- ```input[type=checkbox]``` 엘리먼트의 값이 변경되면 ```onChange``` 이벤트가 발생한다.
- ```onChange``` 이벤트가 이벤트 핸들러 함수인 ```handleChecked```를 호출하고, 이 함수가 ```setIsChecked``` 를 호출한다.  
- ```setIsChecked```가 호출되면 호출된 결과에 다라 ```isChecked```변수가 갱신된다.  
- React는 새로운 ```isChecked``` 변수를 ```CheckboxExample``` 컴포넌트에 넘겨 해당 컴포넌트를 다시 렌더링 한다. 

```javascript
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };
  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={handleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}
```

### Precautions
- React 컴포넌트는 state가 변경되면 새롭게 호출되고, 리렌더링 된다.  
- React state는 상태 변경 함수 호출로 변경해야한다. 즉, 강제로 변경을 시도하면 안된다.  

상태 변경 함수 사용은 React와 개발자의 약속이다.  
강제로 변경을 시도하면, 리렌더링이 되지 않는다거나, state가 제대로 변경되지 않는다.  

```javascript
// 이러면 안된다!!!

function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const forceHandleChecked = (event) => {
    // setIsChecked(event.target.checked);
    isChecked = true;
  };
  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={forceHandleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}
```

## Event Handling
React의 이벤트 처리 (이벤트 핸들링; Event handling) 방식은 DOM의 이벤트 처리 방식과 유사하다.  
단, 몇 가지 문법 차이가 있다.  

- React에서 이벤트는 소문자 대신 카멜 케이스 (camelCase) 를 사용한다.
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 처리함수(이벤트 핸들러; Event handler)를 전달한다.  

HTML과  React의 이벤트 처리 방식차이는 아래와 같다.  
``` javascript
// HTML
<button onclick="handleEvent()">Event</button>

// React
<button onClick={handleEvent}>Event</button>
```

이벤트를 처리하는 데 여러 방식이 가능하다. 다음은 자주 사용되는 이벤트 처리에 대한 예시이다.
### onChange
```<input>``` ```<textarea>``` ```<select>```와 같은 폼(Form) 엘리먼트는 사용자의 입력값을 제어하는데 사용된다.  
React에서는 이러한 **변경될 수 있는 입력값**을 일반적으로 **컴포넌트의 state**로 관리하고 업데이트한다.  
```onChange```이벤트가 발생하면, ```e.target.value```를 통해 이벤트 객체에 담겨있는 ```input```값을 읽어올 수 있다.  
컴포넌트 return문 안의 ```input```태그에 ```value```와 ```onCHange```를 넣은 예시이다.  
```onChange```는 ```input```의 텍스타가 바뀔 때 마다 발생하는 이벤트이다.  
이벤트가 발생하면 ```handleChange```함수가 작동하며, 이벤트 객체에 담긴 ```input```값을 ```setState```를 통해 새로운 **state**로 갱신한다.

```javascript
function NameForm() {
    const [name, setName] = userState("");

    const handleChange = (e) => {
        setName(e.target.value);
    }

    return (
        <div>
            <input type = "text" value={name} onChange={handleChange}></input>
            <h1>{name}</h1>
        </div>
    );
};
```


### onClick
```onClick``` 이벤트는 사용자가 클릭이라는 행동을 하였을 때 발생하는 이벤트이다.  
버튼이나, ```<a>``` 태그를 통한 링크 이동 등과 같이 사용할 수 있다.  
위의 예시에서 ```onChange```에 버튼을 추가하여, 클릭시 ```input``` 태그에 입력한 이름이 alert를 통해 알림창이 팝업되도록 만들어보자.  

```javascript
// 잘못된 예시!

function NameForm() {
    const [name, setName] = userState("");

    const handleChange = (e) => {
        setName(e.target.value);
    }

    return (
        <div>
            <input type = "text" value={name} onChange={handleChange}></input>

            // 추가한 부분~
            <button onClick={alert(name)}>Button</button>

            <h1>{name}</h1>
        </div>
    );
};
```

위처럼 ```onClick```이벤트에 alert(name) 함수를 바로 호출하면 컴포넌트가 렌더링될 때 함수 자체가 아닌,  
함수 자체의 호출 결과가 ```onClick```에 적용된다.  
때문에 버튼을 클릭할 때가 아닌, 컴포넌트가 렌더링 될 때에 alert이 실행되고,  
다라서 그 결과인 undefined (함수는 리턴값이 없을 떄 undefined를 반환한다.)가 ```onClick```에 적용되어, 클릭했을 때 아무런 결과가 일어나지 않는다.  
다라서 ```onClick``` 이벤트에 함수를 전달 때는 함수를 호출하는 것이 아니라,  
아래와 같이 리턴문 안에서 함수를 정의하거나, 리턴문 외부에서 함수를 정의 후, 이벤트에 함수 자체를 전달해야한다.  
단, 두가지 방법 모두 arrow function을 사용하여 함수를 정의하여야, 해당 컴포넌트가 가진 state에 함수들이 접근할 수 있다.  

```javascript
function NameForm() {
    const [name, setName] = userState("");

    const handleChange = (e) => {
        setName(e.target.value);
    }

    const handleClick = () => {
        alert(name);
    };

    return (
        <div>
            <input type = "text" value={name} onChange={handleChange}></input>
            <button onClick={handleClick}>Button</button>
            <h1>{name}</h1>
        </div>
    );
};
```

## Practice
- Select  

```select tag```는 사용자가 drop down 목록을 열어 그 중 한가지 옵션을 선택하면, 선택된 옵션이 state 변수에 갱신된다.  
```useState```가 어떠한 상태를 갱신하도록 설정되어있는지 확인해보자.  

```javascript
import React, { useState } from "react";
import "./styles.css";

function SelectExample() {
  const [choice, setChoice] = useState("apple");

  const fruits = ["apple", "orange", "pineapple", "strawberry", "grape"];
  const options = fruits.map((fruit) => {
    return <option value={fruit}>{fruit}</option>;
  });

  console.log(choice);

  const handleFruit = (event) => {
    setChoice(event.target.value);
  };

  return (
    <div className="App">
      <select onChange={handleFruit}>{options}</select>
      <h3>You choose "{choice}"</h3>
    </div>
  );
}

export default SelectExample;
```

- Pop up  

Pop up은 open과 close를 state를 통해 관리할 수 있다.
```javascript
import React, { useState } from "react";
import "./styles.css";

function App() {
  const [showPopup, setShowPopup] = useState(false);

  const togglePopup = () => {
    // 클릭을 하면 토글해주자!
    setShowPopup(!showPopup);
  };

  return (
    <div className="App">
      <h1>Fix me to open Pop Up</h1>
      <button className="open" onClick={togglePopup}>
        Open me
      </button>
      {showPopup ? (
        <div className="popup">
          <div className="popup_inner">
            <h2>Success!</h2>
            <button className="close" onClick={togglePopup}>
              Close me
            </button>
          </div>
        </div>
      ) : null}
    </div>
  );
}

export default App;
```

## Controlled Component
React가 state를 통제할 수 있는 컴포넌트를 Controlled Component라고 한다.  
제어 컴포넌트가 동작하는 순서는 아래와 같다.  
- 사용자가 input에 값을 입력한다. 
- 사용자가 값을 입력할 때마다 ```onChange``` 이벤트 핸들러가 발생하여, ```set```메서드를 통해 state 값을 변경한다.
- 변경된 state 값을 input value에 할당한다.

제어 컴포넌트를 사용하면, 입력 값이 생길 때마다 상태를 새롭게 갱신하여 항상 최신값으로 유지할 수 있다.  
즉, 데이터와 UI에서 입력한 값이 항상 동기화 되고 있음을 알 수 있다.  

```javascript
import "./styles.css";
import React, { useState } from "react";

export default function App() {
  const [username, setUsername] = useState("");
  const [msg, setMsg] = useState("");

  return (
    <div className="App">
      <div>{username}</div>
      <input
        type="text"
        value={username}
        onChange={(event) => setUsername(event.target.value)}
        placeholder="여기는 인풋입니다."
        className="tweetForm__input--username"
      ></input>
      <div>{msg}</div>
      <textarea
        placeholder="여기는 텍스트 영역입니다."
        className="tweetForm__input--message"
        onChange={(event) => setMsg(event.target.value)}
        value={msg}
      ></textarea>
    </div>
  );
}
```

## React Data Flow
React의 개발 방식의 가장 큰 특징은 페이지 단위가 아닌, 컴포넌트 단위로 시작한다는 점이다.  
FE 개발자는 앱의 프로토타임을 받으면, 먼저 컴포넌트를 식별한다.  
그렇게 컴포넌트를 만들고, 다시 페이지를 조립해 나간다.  
이러한 개발 방식을 Bottom-Up, 즉 상향식 개발이라고 한다.  
상향식 개발의 큰 장점은 테스트가 쉽고 확장성이 좋다는 점이다.  
  
컴포넌트를 나눌 때에는 단일 책임 원칙에 다라 구분한다.  
하나의 컴포넌트는 한 가지 일만 하도록 하자.  

### Top-Down dataflow
컴포넌트는 컴포넌트 바깥에서 props를 이용해 데이터를 마치 전달인자 (arguments) 혹은 속성 (attrivbutes) 처럼 전달 받을 수 있다.  
데이터를 전달하는 주체는 부모 컴포넌트가 된다.  
이는 데이터 흐름이 Top-Down, 즉 하향식임을 의미한다.  
  
one-way data flow, 단방향 데이터 흐름이 React를 대표하는 키워드일 정도로 이 원칙은 매우 중요하다.  
컴포넌트는 props를 통해 전달받은 데이터가 어디서 왔는지 알지 못한다.  

### State data definition
어플리케이션에서 필요한 데이터가 무엇인지 먼저 정의해야한다.  
변하는 값과 변하지 않는 값이 무엇인가?  
변하는 값들은 state로 정의한다.  
  
다음과 같은 기준으로 state 데이터인지 아닌지 구분해보자.
- 부모로부터 props를 통해 전달되는가?
- 시간이 지나도 변하지 않는가?
- 컴포넌트 안의 다른 state나 props를 가지고 계산가능한가?
이들 중 하나라도 만족한다면 state가 아니다.  

### Location of State
상태가 특정 컴포넌트에서만 유의미하다면, 특정 컴포넌트에만 위치시키면 된다.  
하지만, 만일 하나의 상태를 기반으로 두 컴포넌트가 영향을 받는다면, 이때에는 공통 소유 컴포넌트를 찾아 그곳에 상태를 위치해야 한다.  
즉, 두 개의 자식 컴포넌트가 하나의 상태에 접근하고자 할 때는 두 자식의 공통 부모 컴포넌트에 상태를 위치해야 한다.  

### Reversed Data FLow
부모 컴포넌트에서의 상태가 하위 컴포넌트에 의해 변하는 액션은, 부모의 상태를 변화시켜야 한다.  
하지만, 하위 컴포넌트에서의 클릭 이벤트가, 부모의 상태를 바꿔야만 하는 상황이 있다.  
이를 Lifting state up, State 끌어올리기 라고 한다.  
  
이는 상태를 변경시키는 함수 handler를 하위 컴포넌트에 props로 전달해서 해결할 수 있다.  
이는 마치 콜백 함수를 사용ㅎ아는 방법과 비슷하다.  