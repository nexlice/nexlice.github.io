---
title: API Server
tags: 
 - node.js
 - API Server
 - nodemon
 - Visuial Studio Code
 - Postman

description: Learn about debugging Node.js Server!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->

# Node app Debugging
`Node.js`로 구동되는 서비스를 디버깅하는 방법에 대해 알아보자.  

---  

## Browser
서버 디버깅을 할 때, `console.log`만으로 디버깅할 때에는 매우 귀찮은 일이다.  
이때 command line에서 `inspect` 옵션을 활용해볼 수 있다.  
자세한 내용은 [여기](https://nodejs.org/en/docs/guides/debugging-getting-started)를 보자.  

```bash
node --inspect basic-server.js
```

`inspect`옵션을 넣어서 실행해주면, 디버거가 실행된다.  
크롬 브라우저에서 개발자도구를 열면 node 아이콘이 등장한다.  
~~사파리는 안되는 것 같다...~~  
이제 `Postman`이나, 어플리케이션에서 리퀘스트를 보내면 트리구조로 브라우저 콘솔에 나타난다.  
<br>  

만약 user code가 시작하기 전에 디버거를 걸고 싶으면, `--inspect-brk`옵션을 넣어준다.  
시작하자마다 break point가 걸리기때문에, line by line debugging이 가능하다.  
`nodemon`도 모든 디버깅 옵션을 지원한다.  

---  

## Visual Studio Code
`VS Code`에서도 원하는 코드 라인에 break point를 걸고, 왼쪽 Debugger 탭에서 콘솔을 통해 디버깅이 가능하다.  
`VS Code`가 자동으로 `npm start`를 하는 설정이기 때문에 `package.json`을 알맞게 수정해야 정상 작동이 가능하다.  
```javascript
"scripts" :{
    start: "nodemon --inspect-brk server/basic-server.js",
    ...
}
```

만약 `package.json`을 바꾸고 싶지 않다면, 디버거 > 구성추가 에서 원하는 구성을 작성하여도 좋다.  

---

## nodemon and Postman
`nodemon`을 설치하면 `live server`와 같이 서버 소스를 고쳤을 때 바로 적용(hot reloading)이 되게할 수 있다.  
또한 `postman`을 통해서 client의 요청을 쉽게 테스팅할 수 있다.  

---  

### Installation & Execution
```bash
npm -g install nodemon
nodemon basic-server.js
```