---
title: JavaScript Runtime
tags: 
 - JavaScript
 - javasScript Runtime
 - node.js
 - module
 - nvm
 - npm
description: Learn about JavaScript Runtime!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

# Runtime
런타임이란 프로그래밍 언어가 구동되는 환경이다.  
어떤 프로그램이 동작할 때, 프로그램이 동작하는 곳을 런타임이라 한다.  

---
## What is JavaScript Runtime?
우리는 이미 자바스크립트 런타임을 사용하고 있다.  
크롬, 사파리같은 웹 브라우저가 바로 자바스크립트 런타임이다!  

---
## Types of JavaScript Runtime
웹 브라우저가 대표적인 자바스크립트 런타임이다.  
이전에는 웹 브라우저밖에 없었으나, **node.js**이란 새로운 자바스크립트 런타임의 등장으로,  
자바스크립트가 브라우저가 아닌 곳에서 실행될 수 있기 되었다.  
이제 자바스크립트를 이용해서 웹페이지 뿐 아니라 서버와 같은 다른 프로그램을 만들 수 있다.  

---
### Node.js
노드.js 런타임의 등장으로. 자바스크립트 코드를 브라우저와 node.js 환경 모두에서 실행시킬 수 있다.  
HTML `<script>` 태그 내에 자바스크립트 코드를 작성하면, 이 코드는 웹브라우저에서 작동한다.  
CLI 환경에서 `node <file_name>` 명령어를 프롬프트에 입력하면, 작성한 코드가 node.js라는 런타임에서 실행된다.  

---
#### nvm
nvm은 node version manager의 이니셜이다.  
자주 나오는 용어인 lts는 long tern service의 이니셜이다.  
  
개발을 하다보면 node.js의 다양한 버전에 대응해야할 경우가 있다.  
~~실제로 리액트를 실행시킬 때 최신 버전의 node 버전으로 하면 실행되지 않는 경우가 종종 있다.~~  
nvm을 통해 다양한 노드 버전을 옮겨다닐 수 있다.  

---
#### module
모듈이란 컴증된 코드를 말한다.  
"바퀴를 재발명하지 마라"라는 프로그래밍 세계에서의 격언이 있듯, 개발을 할 때 모든 것을 다 만들어서 쓰지 않는다.  
  
다 만들지 않는 이유는 여러가지가 있다.  
시간이 많이 걸리고, 우리가 만든것을 100% 신뢰하기가 어렵기 때문이다.  

이러한 모듈을 node.js에서는 npm module이라 부른다.  
이에 대한 정보를 담아둔 곳이 package.json이다.  

---
### package.json
package.json에는 이 프로그램을 실행시키기 위해 필요한 모듈이 무엇인지,  
프로그램을 실행시키는 방법, 그리고 프로그램을 테스트하는 방법 등이 명시되어있다.  
아래는 package.json의 예시이다.  

```javascript
{
    // informations about the project.
    "name" : "hello",
    "version": "1.0.0",
    "description" : "",

    "main" : "index.js"

    // commands available at CLI
    "scripts" : {
        "test" : "hello/*.js --sort",
        "report" : "hello/*.js --sort -- reporter",
        "submit" : "codestates-submission"
    },
    "keywords":[],

    // dependencies about the development.
    "dependencies":{
        "@codestates-cc/submission-npm" : "^1.1.1"
    },
    "devDependencies":{
        "chai" : "^4.2.0"
    }
}
```
헷갈리면 안 되는 점은,  
이 프로그램을 실행시키기위해 필요한 실제 모듈은 따로 `node_modules` 이라는 폴더에 저장된다는 것이다.  
`package.json`에는 어떤 모듈인지만 적혀있다.  

---
#### Advantages of package.json
프로젝트 코드를 전달할 때, 포함하고있는 모든 모듈을 다 전달하지 않아도 된다는 점이 장점이다.  
우리는 프로젝트 코드를 넘길 때, 
필요한 모듈은 `package.json`에 적어놓았으니 직접 다운받아서 써라! 라고 하면 된다.  
`npm install` 명령어를 입력하면 `package.json`에서 필요하다고하는 모듈을 다운로드한다.   
`npm install`이 완료되면 `node_modules` 디렉토리가 생긴다.  

---
### devDependencies
`dependencies`는 모듈이라 생각해도 좋다.  
개발이나 실행에 해당 모듈을 의존한다고 해서 **의존성**이라고 부른다.  
`devDependencies`에는 이 프로젝트를 개발하는 환경에서 필요한 모듈들이 무엇인지가 적혀있다.  
예를 들면 코드 모양을 잡아주는 lint나, 테스팅 모듈처럼,  
실제 프로젝트 동작에 직접적으로 영향을 주지 않는 모듈을 명시한다.  

---
#### npm install <모듈명> --save-dev
`--save-dev` 옵션과 함꼐 설치하면 자동으로 `devDependencies`에 추가된다.  

---
### dependencies
이 프로젝트가 돌아가기 위해 반드시 필요한 모듈들이 무엇인지 적혀있다.  
`underscore`, `react`같은 것들이다.  

---
#### save option
이 옵션과 함께 설치하면 자동으로 `dependencies`에 추가 된다.  
하지만 `npm5`부터는 `--save` 옵션을 기본 옵션으로 적용한다.  
즉, `--save`를 사용하지 않아도 `dependencies`에 항목이 추가된다.  
즉, `--save`옵션은 생략해도 좋다.  

---
### Why package.json?
내가 만든 프로젝트라면, 이 프로젝트에 어떤 모듈이 필요하고, 어떻게 실행시킬지를 잘 안다. ~~모를지도...?~~
하지만 프로젝트를 처음 접하는 사람이 실행시킬 때에는, 바로 알 수 없다.  
협업을 하기 위해서. 프로젝트에 대해 알려주기 위해 `package.json`을 쓴다.  

---
### scripts
`scripts` 항목은 CLI에서 사용 가능한 명령을 기술한다.  
우리는 이를 `npm script`라고 부른다.
cli에서 실행할 때에는 다음과 같이 실행한다.  
```bash
npm run <스크립트 이름>
```

---
### 예제
주로 실행, 테스트, 코드검사(lint) 등을 한다.  
이러한 작업이 항상 모든 프로젝트에 있는 것은 아니며,  
테스트 케이스 통과만이 목적인 경우에는 `start` 스크립트조차 없을 수 있다.  

```bash
npm run start
npm run test
npm run lint
```