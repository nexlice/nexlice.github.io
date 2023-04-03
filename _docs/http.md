---
title: HTTP
tags: 
 - HTTP
 - Web
 - Server
 - Client
 - URL
 - URI
 - IP
 - Port
 - DNS
 - domain
 - XHR
 - fetch
 - REST API
 - SSR
 - CSR
 - CORS

description: Learn about the concept of HTTP!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

{% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %}

# Advanced Web
이 챕터에서는 HTTP와 브라우저의 작동 원리에 대해서 정리한다.  
API의 대표적인 아키텍처인 REST API를 알아보고, 이를 활용하는 방법을 알아본다.  

앞으로 설명할 글에서 나오는 용어들을 정리하였다.  
**Client**  
사용자가 볼 수 있는 화면, 사용자와 상호작용할 수 있는 곳.  
혹은 리소스를 사용하는 어플리케이션.  
모든 클라이언트가 항상 GUI의 형태를 가지진 않는다.  

**Server**  
눈에 보이지 않지만, 데이터를 전달해 주거나, 로직을 수행하는 곳.  
리소스가 존재하는 곳.  

**2 Tier Architecture**  
클라이언트 - 인터넷 - 서버 구조.  
클라이언트와 서버가 물리적으로 구분되어있고, 이 둘 사이를 인터넷이 연결하는 형태이다.  

**3 Tier Architecture**  
클라이언트 - 서버 - 데이터베이스 구조이다.  
2 Tier Architecture의 기능을 확장한 형태.  
계층이 더 나뉘어졌으므로 관심사 분리의 효과를 가진다.  

## URL vs URI
브라우저의 주소창에 입력한 URL은 서버가 제공되는 환경에 존재하는 파일의 위치를 나타낸다.  
`CLI`환경에서 폴더와 파일의 위치를 찾아 이동하듯이, 슬래시 `/`를 이용하여 서버의 폴더에 진입하거나, 파일ㅇ을 요청할 수 있다.  
그러나 기본적인 보안의 일환으로 외부에서 직접 접근이 가능한 경우는 거의 없다.  
브라우저의 검색창을 클릭하면 나타나는 주소가 URI이다.  
URL는 URL을 포함하는 상위 개념이다.  

#### URL
`URL`은 `Uniform Resource Locator`의 줄임말로, 네트워크 상에서 웹 페이지, 이미지, 동영상 등의 파일이 위차한 정보를 나타낸다.  
`URL`은 scheme, hosts, ulr-path로 구분할 수 있다.  

가장 먼저 작성하는 scheme은 통신 방식(프로토콜)을 결정한다.  
일반적인 웹 브라우저에서는 http(s)를 사용한다.  
hosts는 웹 서버의 이름이나 도메인, IP를 사용하며 주소를 나타낸다.  
url-path는 웹 서버에서 지정한 루트 디렉터리부터 시작하여 접근하고자하는 파일의 경로와 파일명을 나타낸다.  

#### URI
URI는 Uniform Resourse Identifier의 줄임말로,  
일반적으로 URL의 기본 요소인 scheme, hosts, url=path에 더해, query, bookmark를 포함한다.  
query는 웹 서버에 보내는 추가적인 질문이다.  

|부분|명칭|설명|
|:---:|:---:|:---:|
|`file://`, `http://`. `https://`|scheme|통신 프로토콜|
|`127.0.0.1`, `www.google.com`|hosts|데이터 파일이 위치한 웹 서버, 도메인 또는 IP|
|`:80`, `:433`, `:3000`|port|웹 서버에 접속하기 위한 통로|
|`/search`. `/Users/username/Desktop`|url=path|웹 서버의 루트 디렉토리로부터 데이터 파일 위치까지의 경로|
|`q=JavaScript`|query|웹 서버에 전달하는 추가 질문|

> `127.0.01`은 로컬 PC를 나타낸다.

### IP
특정 PC의 주소를 나타내는 체계를 IP address(Internet Protocol address)라고 한다.  
IP는 Internet Protocol의 줄임말로, 인터넷 상에서 사용하는 주소체계를 의미한다.  
인터넷에 연결된 모든 PC는 IP주소 체계를 따라 `.`으로 나뉜 4 덩어리의 숫자로 구분된다.  
이러한 IP주소 체계를 IPv4라고 한다.  
IPv4는 Internet Protocol version 4의 줄임말로, IP 주소 체계의 네번째 버전을 뜻한다.  
IP 주소를 확인하는 명령어로는 `nslookup`이 있다.  
IPv4는 각 덩어리마다 0 부터 255까지 숫자를 나타낼 수 있다.  
이들을 총 조합하면 약 43억개의 IP주소를 표현할 수 있지만, 그 중 몇가지는 용도가 정해져 있다.  

- `localhost`, `127,0,01` : 현재 사용 중인 로컬 PC.
- `0.0.0.0`, `255.255.255.255` : broadcast address, 로컬 네트워크에 접속된 모든 장치와 소통하는 주소.  
서버에서 접근 가능 IP 주소를 broadcast address로 지정하면, 모든 기기에서 서버에 접근할 수 있다.  

개인 PC의 보급으로 IPv4로 할당할 수 있는 PC가 한계를 넘어서고 있다.  
이를 해결하기 위해 나온 것이 IPv6이다.  
IPv6은 표기법을 달리 책정하여 2^(128)개의 IP주소를 표현할 수 있다.  

### PORT
`127.0.0.1:3000` 주소에서 보이는 `:3000`이 포트이다.  
포트는 IP주소가 가리키는 PC에 접속할 수 있는 통로(채널)을 의미한다.  
이미 사용 중인 포트는 중복해서 사용할 수 없다.  
포트 번호는 0~65, 535까지 사용할 수 있다.  
그 중에서 0~1024번까지의 포트 번호는 주요 통신을 위한 규약에 따라 이미 정해져 있다.  
그 중에서 반드시 알아야할 포트는 다음과 같다.  

- 22: SSH
- 80 : HTTP
- 443 : HTTPS  

> 더 많은 포트에 관한 내용은 다음 링크에서 확인하자.  
> [List of TCP and UDP port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)   


### Domain name
웹 브라우저를 통해 특정 사이트에 진입할 때, IP주소를 대신하여 사용하는 주소가 있다.  
- Domain name : codestates.com
- IP Adress : 15.165.183.216  

### DNS
네트워크상에 존재하는 모든 PC는 IP주소가 있다.  
그러나 모든 IP주소가 도메인 이름을 가지는 것은 아니다.  
로컬 PC를 나타내는 `127.0.01`은 `localhost`로 사용할 수 있지만,  
그외의 모든 도메인 이름은 일정 기간동안 대여하여 사용한다.  
이렇게 대여한 도메인 이름과 IP주소를 매칭하기 위해서, 해당 도메인 이름과 매칭된 IP주소를 확인하는 작업을 수행해야한다.  
네트워크에는 이 일을 위한 서버가 별도로 있다.  
DNS는 Domain Name System의 줄임말로, 호스트의 도메임 이름을 IP주소로 변환하거나,  
반대의 경우를 수행할 수 있도록 개발된 데이터베이스 시스템이다.  
- naver.com 입력 : DNS에서 IP 주소 `125.209.222.142` 반환


### HTTP
HTTP는 HyperText Transfer Protocol의 줄임말로, HTML과 같은 문서를 전송하기 위한 `Application Layer` 프로토콜이다.  
HTTP는 웹 브라우저와 웹 서버의 소통을 위해 디자인 되었다.  
전통적인 클라이언트-서버 모델에서 클라이언트가 HTTP messages 양식에 맞춰 요청을 보내면,  
서버도 HTTPs messages 양식에 맞춰 응답한다.  
HTTP는 특정 상태를 유지하지 않는 특징이 있다.  
이러한 특징을 `Stateless(무 상태성)` 라 한다.  

#### HTTP messages
HTTP messages는 클라이언트와 서버 사이에서 데이터가 교환되는 방식이다.  
HTTP messages에는 다음과 같은 두가지 유형이 있다.  

- 요청 (Requests)
- 응답 (Responses)  

HTTP messages는 몇 줄의 텍스트 정보로 구성된다.  
구성파일, API, 기타 인터페이스에서 HTTP messages를 자동으로 완성하기 떄문에,  
개발자는 이런 메세지를 직접 작성할 필요가 거의 없다.  

- HTTP messages의 구조
![HTTP messages의 구조]()

요청(Requests)과 응답(Responses)는 다음과 같은 유사한 구조를 가진다.  
1. start line : startline에는 요청이나 응답의 상태를 나타낸다.  
항상 첫 번째 줄에 위치한다. 응답(Responses)에서는 status line이라 부른다.
2. HTTP headers : 요청을 지정하거나, 메시지에 포함된 본문을 설명하는 헤더의 집합이다.  
3. empty line : 헤더와 본문을 구분하는 빈 줄이 있다.  
4. body : 요청과 관련된 데이터나 응답과 관련된 데이터 또는 문서를 포함한다.  
요청과 응답의 유형에 따라 선택적으로 사용한다.  

이 중 start line과 HTTP headers를 묶어 요청이나 응답의 헤드(head)라고 하고, 페이로드(payload)는 body라고 한다.  

> 페이로드(payload)는 사용에 있어서 전송되는 데이터를 뜻한다.  
> 페이로드는 전송의 근본적인 목적이 되는 데이터의 일부분으로, 그 데이터와 함꼐 전송되는 헤더와 메타데이터와 같은 데이터는 제외한다.  
> 페이로드에 관한 자세한 정의는 [여기](https://ko.wikipedia.org/wiki/페이로드_(컴퓨팅))에서 확인하자.  

#### 요청 (Requests)
HTTP Requests는 Pull protocol로 설명될 수 있다.  
**Start line**  
`Request line`이라고도 부른다.  
HTTP 요청은 클라이언트가 서버에 보내는 메세지이다. Start line에는 세 가지 요소가 있다.  
1. 수행할 작업(GET, PUT, POST 등)이나 방식(HEAD or OPTIONS)을 설명하는 HTTP method를 나타낸다.  
예를 들어 GET method는 리소스를 받아야하고, POST method 는 데이터를 서버로 전송한다.  
2. 요청대상(일반적으로 URL이나 URI) 또는 프로토콜, 포트, 도메인의 절대 경로는 요청 컨텍스트에 작성된다.  
이 요청 형식은 HTTP method마다 다르다.
    - origin 형식 : `?`와 쿼리 문자열이 붙는 절대경로이다. POST, GET, HEAD, OPTIONS등의 method와 함께 사용한다.  
    `POST / HTTP 1.1`  
    `GET /background.png HTTP/1.0`  
    `HEAD /test.html?query=alibaba HTTP/1.1`  
    `OPTIONS /anypage.html HTTP/1.0`  
    - absolute 형식 : 완전한 URL형식으로, 프록시에 연결하는 경우 대부분 GET method와 함꼐 사용한다.  
    `GET http://developer.mozilla.org/en-US/docs/Web/HTTP/Messages HTTP/1.1`  
    - authority 형식 : 도메인 이름과 포트 번호로 이루어진 URL의 authority component이다.  
    HTTP 터널을 구축하는 경우, `CONNECT`와 함께 사용할 수 있다.  
    `CONNECT developer.mozilla.org:80 HTTP/1.1`  
    - asterisk 형식 : `OPTIONS`와 함께 별표(`*`)하나로 서버 전체를 표현한다.  
    `OPTIONS * HTTP/1.1`  
3. HTTP 버전은 메시지의 다른 구조를 결정한다. 이를 위해서 HTTP 버전을 함꼐 입력한다.  

**Headers**  
요청의 Headers는 기본 구조를 따른다.  
대소문자 구분 없는 문자열과 콜론(`:`), 값을 입력한다.  
값은 헤더에 따라 다르다.  
여러 종료의 헤더가 있고, 다음과 같이 그룹을 나눌 수 있다.  
- General headers : 메시지 전체에 적용된다.  
- Request headers : User-Agent, Accept-Type, Accept-Language과 같은 헤더는 요청을 보다 구체화한다.  
Referer처럼 컨텍스트를 제공하거나, If-None과 같이 조건에 따라 제약을 추가할 수 있다.  
-  Entity headers : Content-Length와 같은 헤더는 body에 적용된다.  
body가 비어있는 경우, entity headers는 전송되지 않는다.  
![request headers]()

**Body**  
요청의 본문은 HTTP messages 구조의 마지막에 위차한다.  
모든 요청에 body가 필요하지는 않다.  
GET, HEAD, DELETE, OPTIONS처럼 서버에 리소스를 요청하는 경우에는 본문이 필요하지 않다.  
POST나 PUT과 같은 일부 요청은 데이터를 업데이트하기 위해 사용한다.  
body는 다음과 같이 두 종류로 나눌 수 있다.  
- Single-resource bodies(단일-리소스 본문) : 헤더 두 개(Content-Type과 Content-Length)로 정의된 단일 파일로 구성된다.  
- Multiple-resource bodies(다중-리소스 본문) : 여러 파트로 구성된 본문에서는 각 파트마다 다른 정보를 지닌다.  보통 [HTML form](https://developer.mozilla.org/en-US/docs/Learn/Forms)과 관련이 있다.  



#### 응답(Responses)
**Status line**  
응답의 첫 줄은 Status line이라고 부르며, 다음의 정보를 포함한다.  
1. 현재 프로토콜의 버전 (HTTP/1.1)  
2. 상태 코드 : 요청의 결과를 나타낸다. (200, 302, 404, etc.)  
3. 상태 텍스트 : 상태 코드에 대한 설명  
Status line은 `HTTP/1.1 404 Not Found.`과 같이 생겼다.  

**Headers**  
응답에 들어가는 HTTP headers는 요청(Requests) 헤더와 동일한 구조를 갖고 있다.  
대소문자 구분 없는 문자열과 콜론(`:`), 값을 입력한다.  
값은 헤더에 따라 다르며, 요청의 헤더와 마찬가지로 몇 그룹으로 나눌 수 있다.  
- General headers : 메시지 전체에 적용된다.  
- Response headers: Vary, Accept-Ranges와 같이 상태 줄에 넣기에는 공간이 부족했던 추가 정보를 제공한다.  
- Entity headers: Content-Length와 같은 헤더는 body에 적용된다.  
body가 비어있는 경우, entity headers는 전송되지 않는다.  
![Response headers]()  

**Body**  
응답의 본문은 HTTP messages 구조의 마지막에 위치한다.  
모든 응답에 body가 필요하지는 않다.  
201, 204와 같은 상태 코드를 가지는 응답에는 본문이 필요하지 않다.  
응답의 body는 다음과 같이 두 종류로 나눌 수 있다.  
- Single-resource bodies(단일-리소스 본문)
    - 길이가 알려진 단일0리소스 본문은 두 개의 헤더(Content-Type, Content-Length)로 정의한다.  
    - 길이를 모르는 단일 파일로 구성된 단일-리소스 본문은 Transfer-Encoding이 `chunked`로 설정되어 있으며,  
    파일은 chunk로 나뉘어 인코딩 되어있다.  
- Multiple-resource bodies(다중-리소스 본문) : 서로 다른 정보를 담고 있는 body이다.  

### Stateless
Stateless는 말 그대로 상태를 가지지 않았다는 뜻이다.  
HTTP로 클라이언트와 서버가 통신을 주고 받는 과정에서, HTTP가 클라이언트나 서버의 상태를 확인하지 않는다.  
즉, 클라이언트에서 발생한 모든 상태를 HTTP 통신이 추적하지 않는다.  
이를테면 HTTP 통신은 클라이언트가 로그인하거나 다른 행동하는 것을 알 수 없다.  
만약 쇼핑몰에서 장바구니 담기 버튼을 눌렀을 때, 장바구니에 담긴 상품 정보(상태)를 저장해둬야 한다.  
하지만 HTTP는 통신 규약일 뿐이므로, 상태를 저장하지 않는다.  
따라서, 필요에 따라 다른 방법(쿠키-세션, API, etc.)을 통해 상태를 확인한다.  

#### References
- [MDN: HTTP 요청 메서드](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)  
- [MDN: HTTP 메시지](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages)  
- [MDN: HTTP 상태 코드](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)  

### Further Study
- HTTP's Stateless
- [MIN: MIME Type](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
    - `Content-Type`
- [How does a browser work?](https://d2.naver.com/helloworld/59361)  

## AJAX
AJAX는 Asynchronous JavaScript And XMLHttpRequest의 약자로,  
JavaScript, DOM, Fetch, XMLRequest, HTML 등의 다양한 기술을 사용하는 웹 개발 기법이다.  
AJAX의 가장 큰 특징은 웹 페이지에 필요한 부분에 필요한 데이터만 비동기적으로 받아와 화면에 그려낼 수 있다는 점이다.  
이를테면, 이벤트가 발생할 때마다 Fetch를 통해 데이터를 가져와 업데이트하고 렌더링 하는 것에 사용할 수 있다.  

### Core Functionality
AJAX를 구성하는 핵심 기술은 JavaScript와 DOM, 그리고 Fetch이다.  
전통적인 웹 어플리키에션에서는 `<form>`태그를 이용해 서버에 데이터를 전송해야 했다.  
또한 서버는 요청에 대한 응답으로 **새로운 웹 페이지**를 제공해주어야 했다.  
그러나 Fetch를 사용하면, 페이지를 이동하지 않아도, 서버로부터 필요한 데이터를 받아올 수 있다.  
Fetch는 사용자가 현재 페이지에서 자겁을 하는 동안, 서버와 통신할 수 있도록 한다.  
즉, 브라우저는 Fetch가 서버에 요청을 보내고 응답을 받을 때까지 모든 동작을 멈추는 것이 아니라,  
계속해서 페이지를 사용할 수 있게 하는 비동기적인 방식을 제공한다.  
또한 자바스크립트에서 DOM을 사용해 조작할 수 있기 때문에, Fetch를 통해 전체 페이지가 아닌,  
**필요한 데이터**만 가져와 DOM에 적용시켜 새로운 페이지로 이동하지 않고, 기존 페이지에서 필요한 부분만 변경 가능하다.  

#### XHR vs Fetch
Fetch 이전에는 XHR(XMLHttpRequest)를 사용하였다.  
Fetch는 XHR의 단점을 보완한 새로운 Web API이며, XML보다 가볍고 JavaScript와 호환되는 JSON을 사용한다.  
따라서 오는날에는 XHR보다 Fetch를 많이 사용한다.

```javascript
// Fetch를 사용
fetch('http://52.78.213.9:3000/messages')
    .then(function(response) {
        return response.json();
    })
    .then(function(json) {
        // ...
        }
);
```
Fetch의 등장 이전에는 표준화된 XHR을 사용하였다.  
그러나 XHR은 Cross-Site 이슈 등의 불편함이 있었고,  
그에 비해 Fetch는 간편함, promise 지원 등의 장점을 가지고 있기 때문에, 이제는 Fetch를 사용한다.  
아래는 XMLHttpRequest의 예제이다.  
**Cross-Site 이슈??????**  

```javascript
// XMLHttpRequest를 사용
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://52.78.213.9:3000/messages');

xhr.onreadystatechange = function(){
    if(xhr.readyState !==4) return;
    // readyState 4: 완료

    if(xhr.status === 200){
    // status 200: 성공
        console.log(xhr.responseText): // 서버로부터 온 응답
    } else {
        console.log('에러: ' + xhr.status); // 요청 도중 에러 발생
    }
}

xhr.send(); // 요청 전송
```

이 외에도 Axios와 같은 라이브러리도 존재하며, 경우에 따라 적절한 것을 선택하여 사용한다.  

#### Pros and Cons
**장점**  
- 서버에서 HTML을 완성하여 보내주지 않아도 웹페이지를 만들 수 있다.  
이전에는 서버에서 HTML을 완성하여 보내주어야 화면에 렌더링을 할 수 있었다.  
그러나 AJAX를 사용하면, 서버에서 완성된 HTML을 보내주지 않아도,  
필요한 데이터를 비동기적으로 가져와 브라우저에서 화면의 일부만 업데이트하여 렌더링 가능하다.  
- 표준화된 방법 이전에는 브라우저마다 다른 방식으로 AJAX를 사용했으나,  
XHR이 표준화 되면서부터 브라우저에 상관 없이 AJAX를 사용할 수 있게 되었다.  
- 사용자 중심 어플리케이션 개발 AJAX를 사용하면, 필요한 일부분만 렌더링하기 때문에,  
빠르고, 더 많은 상호작용이 가능한 어플리케이션을 만들 수 있다.  
- 더 작은 대역폭 (네트워크 통신 한 번에 보낼 수 있는 데이터의 크기).  
이전에는 서버로부터 완성된 HTML 파일을 받아와야 했기 떄문에, 한 번에 보내야하는 데이터의 크기가 컸다.  
그러나 AJAX에서는 필요한 데이터를 텍스트 형태(JSON, XML, etc.)로 보내면 되기 때문에, 비교적 데이터의 크기가 작다.  

**단점**  
- Search Engile Optimization(SEO)에 불리하다.  
AJAX 방식의 웹 애플리케이션은 한 번 받은 HTML을 렌더링 한 후,  
서버에서 비동기적으로 필요한 데이터를 가져와 그려낸다.  
따라서, 처음 받는 HTML 파일에는 데이터를 채우기 위한 틀만 작성된 경우가 많다.  
검색 사이트에서는 전 세계 사이트를 크롤링하여, 사용자에게 검색 결과를 보여준다.  
하지만 AJAX 방식의 웹 어플리케이션의 HTML 파일은 뼈대만 있고 데이터는 없기에, 사이트의 정보를 긁어가기 어렵다.  
- 뒤로가기 문제  
일반적으로 사용자는 뒤로가기 버튼을 누르면 이전 상태로 돌아갈 것으로 예상하지만,  
AJAX에서는 이전 상태를 기억하지 않기 떄문에, 사용자가 의도한 대로 동작하지 않는다.  
따라서 뒤로가기 기능을 구현하기 위해서는 별도의 History API를 사용해야 한다.  

### Reference
[지메일이 핫메일을 이긴 진짜 이유 : AJAX가 가져온 유저 인터페이스의 혁신](https://sungmooncho.com/2012/12/04/gmail-and-ajax/)  


## SSR vs CSR
이번 챕터에서는 SSR(Server Side Rendering)과 CSR(Client Side Rendering)의 차이를 설명한다.  

### SSR
![SSR]()  
SSR은 Server Side Rendering의 줄임말이다.  
웹 페이지를 브라우저에서 렌더링하는 대신에, 서버에서 렌더링 한다.  
브라우저에서 서버의 URI로 `GET`요청을 보내면, 서버는 정해진 웹 페이지 파일을 브라우저로 전송한다.  
그리고 서버의 웹 페이지가 브라우저에 도착하면 완전히 렌더링 된다.  
서버에서 웹 페이지를 브라우저로 보내기 전에, 서버에서 완전히 렌더링 했기 때문에 SSR이라 부른다.  
웹 페이지에의 내용에 데이터베이스의 데이터가 필요한 경우, 서버는 데이터베이스의 데이터를 불러온 다음,  
웹 페이지를 완전히 렌더링 된 페이지로 변환한 후에 브라우저에 응답으로 보낸다.  
웹 페이지를 살펴보면 사용자가, 브라우저의 다른 경로로 이동한다면,  
브라우저가 다른 경로로 이동할 때마다 서버는 이 작업을 다시 수행한다.  

### CSR
![CSR]()
CSR은 Client Side Rendering을 의미한다.  
일반적으로 CSR은 SSR의 반대로 여겨진다.  
SSR이 서버 측에서 페이지를 렌더링 한다면, CSR은 클라이언트에서 페이지를 렌더링 한다.  
웹 개발에서 사용하는 대표적인 클라이언트는 웹 브라우저이다.  
브라우저의 요청을 서버로 보내면, 서버는 웹 페이지를 렌더링하는 대신,  
웹 페이지의 골격이 될 단일 페이지를 클라이언트에 보낸다.  
이떄 서버는 웹 페이지와 함꼐 JavaScript 파일을 보낸다.  
클라이언트가 웹 페이지를 받으면, 웹 페이지와 함꼐 전달된 JavaScript 파일은,  
브라우저에서 웹 페이지를 완전히 렌더링 된 페이지로 바꾼다.  
웹 페이지에 필요한 내용이 데이터베이스에 저장된 데이터인 경우에는,  
블라우저가 데이터베이스에 저장된 데이터를 가져와서 웹 페이지에 렌더링 해야한다.  
이를 위해 API가 사용된다.  
즉, 웹 페이지를 렌더링 하는 데에 필요한 데이터를 API 요청으로 해소한다.  
또한 브라우저가 다른 경로로 이동한다면, CSR에서는 SSR과 다르게,  
서버가 웹 페이지를 다시 보내지 않는다.  
브라우저는 브라우저가 요청한 경로에 따라 페이지를 다시 렌더링한다.  
이떄 보이는 웹 페이지의 파일은 맨 처음 서버로부터 잔달받은 웹 페이지 파일과 동일한 파일이다.  

### The Difference
CSR과 SSR의 주요 차이점은, 페이지가 렌더링 되는 위치이다.  
SSR은 서버에서 페이지를 렌더링하고,  
CSR은 브라우저(클라이언트)에서 페이지를 렌더링한다.  
브라우저는 사용자가 다른 경로를 요청할 때마다 페이지를 새로고침하지 않고, 동적으로 라우팅을 관리한다.  

### Usage
**SSR**  
- [SEO(Search Engine Optimination)](https://en.wikipedia.org/wiki/Search_engine_optimization)이 우선순위인 경우, 일반적으로 SSR을 사용한다.  
- 웹 페이지의 첫 화면 렌더링이 빠르게 필요한 경우에도, 단일 파일 용량이 작은 SSR이 적합하다.  
- 웹 페이지가 사용자와 상호작용이 적은 경우, SSR을 활용한다.  

**CSR**  
- SEO가 우선순위가 아닌 경우, CSR을 이용할 수 있다.  
- 사이트에 풍부한 상호 작용이 있는 경우, CSR은 빠른 라우팅으로 강력한 사용자 경험을 제공한다.  
- 웹 어플리케이션을 제작하는 경우, CSR을 이용해 더 나은 사용자 경험(빠른 동적 렌더링, etc.)을 제공할 수 있다.  

## Browser Security Model
> 이 섹션은 Web administrator들을 위한 글이다.  
웹 보안에는 서버, 데이터베이스, 그리고 클라이언트 보안이 있는데,  
이 중 클라이언트에 속하는 (대부분의 클라이언트가 브라우저를 사용하므로) 브라우저의 보안에 대한 내용이다.  
브라우저의 보안에 대해서는 다음 세가지 내용을 알아야한다.  


- CORS  
- XSS  
- CSRF  

### CORS
CORS는 Cross-Origin Resource Sharing의 이니셜이다.  
CORS는 서로 다른 origin간에 리소스를 공유하는 메커니즘이다.  
추가적인 HTTP 헤더를 이용해서, 브라우저에게 웹 어플래케이션이 어떤 origin의 permission을 갖고있는지 알게 해준다.  
다시 말해, 처음 전송되는 리소스의 도메인과 다른 도메인으로부터 리소스가 요청될 경우,  
해당 리소스는 **cross-origin HTTP 요청**에 의해 요청된다.  
이를테면, `http://domain-a.com`으로부터 전송되는 HTML 페이지가  
`<img> src` 속성을 통해 `http://domain-b.com/image.jpg`를 요청하는 경우가 있다.  
오늘날 많은 웹 페이지들은 CSS, 이미지, 그리고 스크립트와 같은 리소스들을 각각의 출처로부터 읽어온다.  
CORS는 **브라우저만의 자발적인 (브라우저의 어플리케이션을 사용하는) 유저들을 보호하는 정책이다.**  
![CORS flow]()  
위 그림처럼 같은 origin request는 항상 허용한다.  
하지만 다른 origin으로부터 request가 있을 때 (domain-b),  
해당 이미지가 불려질 수도 있고, 불려지지 않을 수 있다.  

#### Usage
다음 리퀘스트들이 CORS를 사용한다.  
- Invocation of `XMLHttpRequest` or `Fetch` APIs in a cross-site manner
- Web Fonts
- WebGL textures
- Images/video frames drawn to a canvas using `drawImage()`

결국 두가지 이상의 도메인으로부터 리소스가 요청될 시, CORS를 사용하게 한다.  
자세한 내용은 [여기](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)를 보자.  


### XSS


### CSRF


## REST API
웹 어플리케이션에서는 HTTP 메서드를 이용해 서버와 통신한다.  
이런 사용은 아무런 규칙 없이 이루어지는 것이 아니다.  
요청과 응답을 할 때, '제대로 보내고 받을 수 있는' 일종의 규약이 존재한다.  
REST는 Representational State Transfer의 아니셜로,  
`Roy Fielding`의 박사 학위 논문에서 웹(http)의 장점을 최대한 활용할 수 있는 아키텍처로써 처음 소개되었다.  
REST API는 *웹에서 사용되는 데이터나 자원(Resource)을 HTTP URI로 표현하고, HTTP 프로토콜을 통해 요청과 응답을 정의하는 방식*을 말한다.  

### RMM
REST API를 작성할 때에는 몇 가지 지켜야할 규칙들이 있다.  
`Roy Fielding`이 논문에서 제시한 REST 방법론을 보다 더 실용적으로 적용하기 위해,  
`Leonard Richardson`은 REST API를 잘 적용하기 위한 4단계 모델을 만들었다.  
![Richardson 성숙도 모델 (RMM)]()

REST 성숙도 모델은 총 4단계 (0~3단계)로 나누어진다.  
앞서 이야기한 `Roy Fielding`은 이 모델의 모든 단계를 충족해야 REST API라고 부를 수 있다고 주장했다.  
그러나 실제로 엄밀하게 3단계까지 지키기 어렵기 때문에 2단계까지만 적용해도 좋은 API 디자인이라 볼 수 있따.  
이런 경우 HTTP API라고도 부른다.  

#### REST 성숙도 모델 - 0단계
0단계에서는 단순히 HTTP 프로토콜을 사용하기만 해도 된다.  
이 경우, 해당 API를 REST API라고 할 수는 없으며, 0단계는 좋은 REST API를 작성하기 위한 기본 단계이다.  
![0단계]()  

#### REST 성숙도 모델 - 1단계
REST 성숙도 모델에 따르면, 1단계에서는 개별 리소스와의 통신을 준수해야한다.  
REST API는 웹에서 사용되는 모든 데이터나 자원(Resource)을 HTTP URI로 표현하기 때문에,  
모든 자원은 개별 리소스에 맞는 엔드포인트(Endpoint)를 사용해야하고,  
요청하고 받은 자원에 대한 정보를 응답으로 전달해야한다.  
앞선 0단계에서는 모든 요청에서 엔드포인트로 `/appointment`를 사용했다.  
하지만 1단계에서는 요청하는 리소스가 무엇인지에 따라 각기 다른 엔드포인트로 구분하여 사용해야 한다.  
![1단계]()  
예시와 같이, 어떤 리소스를 변화시키는지 혹은 어떤 응답이 제공되는지에 따라 각기 다른 엔드포인트를 사용하기 때문에,  
적절한 엔드포인트를 작성하는 것이 중요하다.  
엔드포인트 작성 시에는 동사, HTTP 메서드, 혹은 어떤 행위에 대한 단어 사용은 지양하고,  
리소스에 집중해 명사 형태의 단어로 작성하는 것이 바람직한 방법이다.  

#### REST 성숙도 모델 - 2단계
REST 성숙도 모델 2단계에서는 CRUD에 맞게 적절한 HTTP 메서드를 사용하는 것에 중점을 둔다.  
앞선 0,1단계에서는 모든 요청을 CRUd에 상관없이 POST로 하고 있다.  
그러나 REST 성숙도 모델에 2단계에 따르면, 이는 CRUD에 따른 적합한 메서드를 사용한 것은 아니다.  
응답코드 또한 고려하여 재작성하면 다음과 같다.  
![2단계]()  

메서드를 사용할 떄의 규칙은 다음과 같다.  
- `GET` : 서버의 데이터를 변화시키지 않는 요청
- `POST` : 요청마다 새로운 리소스를 생성한다. 
- `PUT` : 요청마다 같은 리소스를 반환한다.  
> 매 요청마다 같은 리소스를 반환하는 특징을 멱동([idempotent](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent))하다고 한다.  
> 멱등성을 갖는 `PUT`과 `POST`는 구분하여 사용해야 한다.  
- `PUT` : 데이터 전체를 교체한다.  
- `PATCH` : 데이터의 일부를 수정한다.  
더 자세한 내용은 [여기](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)를 확인하자.  

API를 작성할 떄, REST 성숙도 모델의 2단계까지 적용을 하면, 대체로 잘 작성된 API라고 여긴다.  
물론 `Roy Fielding`은 3단계까지 만족하지 못한다면 REST API가 아니기 때문에 HTTP API라고 불러야 한다고 주장하지만,  
모범적인 API 디자인 조차도 REST 성숙도 모델의 3단계까지 적용한 경우는 극히 드물다.  
따라서 3단계까지 무조건 모두 적용해야 한다는 것은 아니다.  

#### REST 성숙도 모델 - 3단계
마지막 단계는 HATEOAS(Hypertext As The Engine Of Application State)라는 약어로 표현되는 하이퍼미디어 컨트롤을 적용한다.  
3단계의 요청은 2단계와 동일하지만, 응답에는 리소스의 URI를 포함한 링크 요소를 삽입하여 작성한다는 것이 다르다.  
이떄 응답에 들어가게 되는 링크 요소는 응답받은 다음에 할 수 있는 다양한 액션들을 위해 많은 하이퍼미디어 컨트롤을 포함한다.  
![3단계]()  
위처럼 어떤 값을 조회 한 후에, 그 시간대에 예약할 수 있는 링크를 삽입하는 등, 새로운 기능에 접근할 수 있도록 하는 것이 3단계의 특징이다.  

### Reference
- [5가지 기본적인 REST API 디자인 가이드](https://blog.restcase.com/5-basic-rest-api-design-guidelines/)
- [호주 정부 API 작성 가이드](https://api.gov.au/sections/getting-started.html)
- [구글 API 작성 가이드](https://cloud.google.com/apis/design?hl=ko)
- [MS의 REST API 가이드 라인](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md)

### Open API
Open API는 누구에게나 열려있는 API이다.  
하지만 무제한으로 이용할 수 있지는 않고, 기관이나 API마다 정해진 이용 수칙이 있다.  

### API Key
API를 이용하기 위해서는 API Key가 필요하다.  
API Key는 서버의 문을 여는 열쇠라고 생각할 수 있다.  
클라이언트의 요청에 따라 서버에서 응답한다는 말은, 서버를 운용하는 데에 비용이 발생한다는 말이다.  
따라서 서버 입장에서 아무런 조건 없이 익명의 클라이언트에게 데이터를 제공할 의무도, 이유도 없다.  
(물론 가끔 API Key가 필요하지 않은 경우도 있다.)  
그래서 로그인된 이용자에게만 자원에 접근할 수 있는 권한을 API Key의 형태로 제공하고,  
데이터를 요청할 때 API Key를 같이 전달해야만, 원하는 응답을 받을 수 있다.  


> 1inch network??

> 디스코드 에 올려주신 tier software architecture

