---
title: Lifting State Up
tags: 
 - react
 - state
 - Pure Function
 - Side Effect
 - useEffect

description: Learn about the concepts of lifting State!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

# Lifting State Up
단반향 데이터 흐름이라는 원칙에 따라, 하위 컴포넌트는 상위 컴포넌트로부터 전달받은 데이터의 형태, 혹은 타입만 알 수 있다.  
데이터가 `state`로부터 왔는지, 하드 코딩으로 입력한 내용인지는 알지 못한다.  
그러므로 하위 컴포넌트에서의 어떤 이벤트로 인해 상위 컴포넌트의 상태가 바뀌는 것은,  
마치 "역방향 데이터 흐름"과 같이 조금 특이하게 들릴 수 있다.  
`React`가 제시하는 해결책은 다음과 같다.  

> 상위 컴포넌트의 "상태를 변경하는 함수" 그 자체를 하위 컴포넌트로 전달하고, 이 함수를 하위 컴포넌트가 실행한다.  

여전히 단방향 데이터 흐름에 부함하는 해결 방법이다.  
그리고 이것을 `상태 끌어올리기`라고 한다.  

```javascript
import React, { useState } from "react";

export default function ParentComponent() {
  const [value, setValue] = useState("날 바꿔줘!");

  const handleChangeValue = () => {
    setValue("보여줄게 완전히 달라진 값");
  };

  return (
    <div>
      <div>값은 {value} 입니다</div>
      <ChildComponent handleButtonClick={handleChangeValue} />
    </div>
  );
}

function ChildComponent({handleButtonClick}) {
  const handleClick = () => {
    // 인자로 받은 상태 변경 함수를 실행한다.
    handleButtonClick();
    // 필요에 따라 설정할 값을 콜백 함수의 인자로 넘길 수도 있다.
    handleButtonClick('자식이 원하는 값을 넘깁니다.');
  };

  return <button onClick={handleClick}>값 변경</button>;
}
```

더욱 실용적인 예제를 [공식문서](https://ko.reactjs.org/docs/lifting-state-up.html)에서 찾을 수 있다.  