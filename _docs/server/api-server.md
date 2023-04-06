# main-page
- node.js
- API Server
- HTTP
- HTTP Request
- HTTP Response
- node.js modules
- Routing
- Express
- CRUD

node.js를 이용하여 백엔드를 구축하는 방법을 알아보고, API Server를 직접 구현해보자.  


# CORS

## Entrance Settings
이전의 클라이언트 서버 관계에서, 유저의 요청에 의해 서버에 있던 클라이언트를 유저가 받아가는 통신을 했다.  
즉, 유저는 서버에 있던 클라이언트(클라이언트에 static하게 담겨있는 데이터)를 일방적으로 보는 방식이었다.  
서버에서 내려준 클라이언트는 서버에 위해가 되는 행동을 하지 않을 것이라 기대했다.  
클라이언트가 요청을 보낼때 보내는 클라이언트도 origin이 서버이고,  
서버가 응답으로 보내는 클라이언트 또한 origin이 서버이기 때문에,  
서버는 이 요청을 막을 필요가 없다.  

하지만, 최근의 웹이 고도화 됨에 따라, SPA(Single Page Application)이 등장하면서,  
한 서버에만 요청하는것이 아니라 여러 서버에 요청을 보내게 되었다.  
즉, 이제는 same origin이 아니라, 다른 origin으로 요청하는 경우가 생겼다.  
이러한 현상을 cross origin resource sharing, CORS라고 한다.  

브라우저에서는 보안상의 이유로, 스크립트 내에서 초기화되는 cross-origin HTTP요청을 제한한다.  
곧이어 개발자들은 브라우저 벤더사들에게 XMLHttpRequest가 cross-domain 요청을 할 수 있도록 요청했다.  
이후, 서버가 허용한 범위 내에서는 cross origin 요청을 허용하도록 브라우저가 변경되었따.  

## defaultCorsHeaders
코드 내에서 defaultCorsHeaders를 만나볼 수 있다.  
다음 예시를 통해 어떤 일을 하는지 알아보자.  
```javascript
const defaultCorsHeaders = {
    'access-control-allow-origin': '*',
    'access-control-allow-methods': 'GET, POST, PUT, DELETE, OPTIONS',
    'access-control-allow-headers': 'content-type, accept',
    'access-control-allow-max-age': 10
};
```

- 모든 도메인(*)을 허용한다.  
- 메서드는 명시된 것만 허용한다.  
- 헤더에는 content-type과 accept만 쓸 수 있다.  
- preflight request는 10초까지 허용 된다.  

## options
options는 preflight request이다.  
브라우저가 자동으로 client가 다른 origin에 있는 서버에 요청할 때, 서버에게 허가를 받는 역할을 한다.  

어떤 서버에서 A origin만 cross-origin domain 요청을 허용한 상황에서,  A가 서버에 POST 요청을 보내는 상황을 가정해보자.
A는 처음에 options라는 preflight request를 통해서 서버에 CORS origin에 대한 request 정보를 확인한다.  
즉, 브라우저가 자동으로 options라는 요청으로 서버로 보내서 CORS origin에 대한 허가를 받은 후에,  
서버에게 POST request를 보내게 된다.  

만약 A가 아닌 B가 서버에게 request를 보낸다고 하면,  
B가 options를 서버에 보냈을 떄 거절 응답이 돌아와 요청이 불가능하다.  

## HTTP Module
다음 `basic-server.js`를 살펴보자.  
HTTP 모듈로 분기를 나누어 서버를 만든 예시이다.  
이 예제는 [여기](https://nodejs.org/ko/docs/guides/anatomy-of-an-http-transaction)를 참고하여 작성하였다.  

```javascript

const http = require('http');
const PORT = 5500;
const ip = 'localhost';

const server = http.createServer((request, response) => {

    // response에 넣을 body.
    let body = [];

    // 요청이 들어왔을 때 여기서 분기를 나눈다.
    if (request.method === 'OPTIONS'){  //preflight request 처리
        //CORS 설정 반환
        response.writeHead(204, defaultCorsHeader);
        response.end();
    }
    else if (request.method === 'POST' && request.url === '/upper'){ //POST이며, url이 /upper일 때
        
        request.on('error', (err) => { // 에러처리
        console.error(err);
        })
        .on('data', (chunk) => { // 데이터를 body에 push
        body.push(chunk);
        })
        .on('end', () =>{ // 여기서 body에 들어간 내용을 가공
        body = Buffer.concat(body).toString().toUpperCase();
        // request method가 OPTIONS일 때 뿐 아니라, 다른 메서드에서도 header를 작성해야 CORS 에러가 나지 않는다.
        response.writeHead(200, defaultCorsHeader); 
        response.end(body);
        });
    }
    else if (request.method === 'POST' && request.url === '/lower'){ //POST이며, url이 /lower일 때
        request.on('error', (err) => {
        console.error(err);
        })
        .on('data', (chunk) => {
        body.push(chunk);
        })
        .on('end', () =>{
        body = Buffer.concat(body).toString().toLowerCase();
        
        // 반복되는 내용은 분기문 밖에서 하고,
        // body = Buffer.concat(body).toString();
        // 분기마다 unique한 내용만 다뤄도 좋다. 
        // body.toLowerCase();
        response.writeHead(200, defaultCorsHeader);
        response.end(body);
        });
    }
    else{
        // 위의 가지가 메서드 이외에는 받지 않고, bad request를 넣어준다.
        response.end("bad request");
    }
    
    console.log(
        `http request method is ${request.method}, url is ${request.url}`
    );

});

const defaultCorsHeader = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
  'Access-Control-Allow-Headers': 'Content-Type, Accept',
  'Access-Control-Max-Age': 10
};

server.listen(PORT, ip, () => {
  console.log(`http server listen on ${ip}:${PORT}`);
});
```

다음 명령어를 통해서 서버를 localhost:5000으로 열 수 있다.
```bash
node basic-server.js 
```

이후 브라우저 주소창에 `localhost:5500/upper`라 치면 GET 메서드로 들어옴을 볼 수 있다.  

## Express
`MERN stack`은 `JavaScript` 생태계에서 인기있는 프레임 워크인 `MongoDB`, `Express`, `React`, `Node`를 지칭하는 말이다.  
이 중 [`Express.js`](https://expressjs.com)는 `Node.js`환경에서 웹 서버, 또는 API 서버를 제작하기 위해 사용되는 인기 있는 프레임 워크이다.  
`Express.js`로 구현한 서버가 http 모듈로 작성한 서버와 다른 점은 다음과 같다.  

- 미들웨어 추가가 편리하다.  
- [자체 라우터](https://expressjs.com/en/guide/routing.html)를 제공한다.  


### Middleware
자동차 공장에서는 컨베이어 벨트 위에 올려진 자동차의 뼈대에, 각 공정마다 부품을 추가한다.  
모든 부품이 추가되면 완성된 자동차가, 어딘가 문제가 있다면 불량품이 결과물로 나오게 된다.  
`미들웨어`는 자동차 고장의 공정과 비슷하다.  
컨베이어 벨트 위에 올라가 있는 request에 필요한 기능을 더하거나,  
문제가 발견된 불량품을 밖으로 걷어내는 역할을 한다.  
`미들웨어`는 `Express.js`의 가장 큰 장점이다.  

#### Frequently used middleware
먼저, 미들웨어를 사용하는 상황은 다음과 같다.  

1. 모든 요청에 대해 URL이나 메서드를 확인할 때  
2. POST 요청 등에 포함된 body(payload)를 구조화할 떄 (또는 쉽게 얻어내고자 할 떄)
3. 모든 요청/응답에 CORS 헤더를 붙여야할 때
4. 요청 헤더에 사용자 인증 정보다 담겨있는지 확인할 때  

미들웨어를 사용하면 `node.js`만으로 구현한 서버에서는 다소 번거로울 수 있는 작업을 더욱 쉽게 적용할 수 있다.  
미들웨어에 대한 [공식문서](https://expressjs.com/ko/guide/writing-middleware.html)를 확인해보자.  

미들웨어는 말 그대로 프로세스 중간에 관여하여 특정 역할을 수행한다.  
위에서 수행했던 실습을 변환해보자.  

#### case 1 : 모든 요청에 대해 URL이나 메서드를 확인할 때  
순수 `node.js` 코드로 작성했을 떄에는 다음과 같이 하였다.  
```javascript
console.log(
    `http request method is ${request.method}, url is ${request.url}`
);
```
로거는 디버깅이나, 서버 관리에 도움이 되기 위해 `console.log`로 적절한 데이터나 정보를 출력한다.  
데이터가 여러 미들웨어를 거치는 동안 응답한 결과를 만들어야 한다면,  
미들웨어 사이사이에 로거를 삽입하여 현재 데이터를 확인하거나, 디버깅에 사용할 수 있다.  
이런 미들웨어는 일반적으로 다음과 같은 구성을 가진다.  
![공식 문서에서 확인할 수 있는 미들웨어의 구성]()  
위 그림은 endpoint가 `/`이면서, 클라이언트로부터 `GET` 요청을 받았을 때 적용되는 미들웨어이다.  
파라미터 순서에 유의하자.  
`req`, `res`는 요청/응답에 해당하고, `next`는 다음 미들웨어를 실행한다.  
다음 그림에서 `next`의 역할을 유추해볼 수 있다.  
![next]()  
다시 첫번째 이미지를 살펴보면, 미들웨어 내부에서는 아무런 작업을 하고있지 않다.  
그저 `next()` 함수를 호출하여 다음 미들웨어로 데이터를 전달하고 있다.  
만약 특정 endpoint가 아니라 모든 요처엥 동일한 미들웨어를 적용하려면, `app.use`를 사용한다.  

```javascript
const express = require('express');
const app = exrpess();

const myLogger = function (req, res, next) {
    console.log('LOGGED'); // 이 부분을 req, res 객체를 이용해 모든 요청에 대한 로그를 찍을 수 있다.
    next();
};

app.use(myLogger);

app.get('/', function (req, res) {
    res.send('Hello World!');
});

app.listen(3000);
```

로그가 정상적으로 작동한다면 다음과 같이 로그가 남게 된다.  
![모든 요청에 대해 메서드와 URL을 출력하는 예시]()

#### case 2 : POST 요청 등에 포함된 body(payload)를 구조화할 때
순수 `node.js`로 HTTP body(payload)를 받을 때에는 `Buffer`를 조합해서 body를 얻을 수 있다.  
즉, 네트워크상의 `chunk`를 합치고, `buffer`를 `body`로 변환하는 작업이 필요하다.

```javascript
let body = [];
request.on('data', (chunk) => {
    body.push(chunk);
}).on('end', () => {
    body = Buffer.concat(body).toString();
    // body 변수에는 문자열 형태로 payload가 담겨져 있따.  
})
```
하지만 [`express.json`](https://expressjs.com/en/api.html#express.json)를 사용하면 이 과정을 간단하게 처리 가능하다.  
> 기존에는 `body-parser` 미들웨어가 필요했지만, `express 4.16`이상 버전부터는 내부에 body-parser가 포함되어 따로 필요가 없어졌다.  

```javascript
app.use(express.json());
app.use(express.urlencoded( {extended : false }));

// ...

app.post('/api/users', function (req, res) {
    // req.body에는 JSON의 형태로 payload가 담겨져 있다.
})

```

#### case 3 : 모든 요청/응답에 CORS 헤더를 붙여아할 때
순수 `node.js` 코드에 CORS 헤더를 붙이려면, 응답 객체의 `writeHead` 메서드 등을 이용하였다.  
이런 메서드를 이용하더라도, `Access-Contrl-Allow-*` 헤더를 매번 재정의 해야한다.  
또한 `OPTIONS` 메서드에 대한 라우팅도 따로 구현해야 했다.  

```javascript
const defaultCorsHeader = {
    'Access-Control-Allow-Origin': '*',
    'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
    'Access-Control-Allow-Headers': 'Content-Type, Accept',
    'Access-Control-Max-Age': 10
};

// ...
if (req.methid === 'OPTIONS') {
    res.writeHead(201, defaultCorsHeader);
    res.end();
}
```

[cors 미들웨어](https://github.com/expressjs/cors)를 사용하면, 이 과정을 다음과 같이 간단하게 처리할 수 있다.  
**모든 요청에 대해 허용**  
```javascript
const cors = require('cors');

// ...
app.use(cors()) // 모든 요청에 대해 CORS를 허용한다.
```

**특정 요청에 대해 허용**  
```javascript
const cors = require('cors');

// ...
// 특정 요청에 대해 CORS를 허용
app.get('/products/:id', cors(), function (req, res, next){
    res.json({msg: 'This is CORS-enabled for a Single Route'})
})
```

#### case 4 : 요청 헤더에 사용자 인증 정보가 담겨있는 지 확인할 때
다음은 HTTP 요청에서 토근이 있는지를 판단하여, 이미 로그인한 사용자일 경우 성공, 아닐 경우 에러를 보내는 미들웨어 예제이다.  

> 토근(Token)이란, 주로 사용자 인증에 사용한다.  

```javascript
app.use((req, res, next) => {
    if(req.headers.token){
        // 토근이 있다면 다음 미들웨어를 수행한다.
        req.isLoggedIn = true;
        next()
    } else {
        // 토근이 없다면 수행하지 않는다.
        res.status(400).send('invalid user')
    }
})
```

#### Router
`Express`는 프레임워크 자체에서 라우터 기능을 제공한다.  
순수 `node.js`에서 분기를 나누어 if-else로 나누어 썼던 것과 달리, 직관적으로 코드를 작성할 수 있다.  
```javascript
const router = express.Router();

router.get('/lower', (req, res) => {
    res.send(data)
})

router.post('/lower', (req, res) => {
    // do something
})
```

### Practice
실습을 최종적으로 모두 `Express`를 이용하여 표현하면 다음과 같이 된다.

```javascript
// Express를 이용한 서버 구현
const express = require('express') // import module
const app = express(); // app that contains middlewares
const cors = require("cors"); // import cors middlware
// Router를 사용하려면 App.js에 따로 설정을 해줘야한다.
// const router = express.Router();
const PORT = 5501;
const ip = 'localhost';

// 정적 파일을 불러와야 브라우저에 HTML 파일을 출력할 수 있다.  
app.use(express.static('client')) // 구현할 파일을 불러온다.
app.use(express.json({strict : false})) // primitive data type도 parsing하도록 허용
app.use(cors()); // 별도의 처리 없이 app.use(cors())를 하면 모든 도메인에서 제한 없이 허용한다.

// 특정 도메인에만 허용하고 싶으면 option 객체를 만들어 파라미터로 넘긴다.
// let options = {
//   origin:"https://domain.com",
//   credentials: true
// }
// app.use(cors(options));

// 로그 기능
const myLogger = function (req, res, next) {
  console.log(`http request method is ${req.method}, url is ${req.url}`)
  next();
};

app.use(myLogger);

app.post('/upper', (req, res) => {
  res.json(req.body.toUpperCase())
})

app.post('/lower', (req, res) => {
    res.json(req.body.toLowerCase())
})

app.listen(PORT, () => {
  console.log(`http server listen on ${ip}:${PORT}`);
});
```

## Node app Debugging
### Browser Degugging
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

만약 user code가 시작하기 전에 디버거를 걸고 싶으면, `--inspect-brk`옵션을 넣어준다.  
시작하자마다 break point가 걸리기때문에, line by line debugging이 가능하다.  

`nodemon`도 모든 디버깅 옵션을 지원한다.  

### Visual Studio Code Debugging
VS Code에서도 원하는 코드 라인에 break point를 걸고, 왼쪽 Debugger 탭에서 콘솔을 통해 디버깅이 가능하다.  
VS Code가 자동으로 `npm start`를 하는 설정이기 때문에 `package.json`을 알맞게 수정해야 정상 작동이 가능하다.  
```javascript
"scripts" :{
    start: "nodemon --inspect-brk server/basic-server.js",
    ...
}
```

만약 `package.json`을 바꾸고 싶지 않다면, 디버거 > 구성추가 에서 원하는 구성을 작서하여도 좋다.  

---

### nodemon & Postman
`nodemon`을 설치하면 `live server`와 같이 서버 소스를 고쳤을 때 바로 적용이 되게할 수 있다.
또한 `postman`을 통해서 client의 요청을 쉽게 테스팅할 수 있다.  

#### Installation & Execution
```bash
npm -g install nodemon
nodemon basic-server.js
```



difference between path variable and query variable

query variable로 준 것은 req.query로 접근 가능하지만
path variable로 준 것은 req.params로 접근해야한다.
https://yusang.tistory.com/70