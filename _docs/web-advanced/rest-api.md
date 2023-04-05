---
title: REST API
tags: 
 - REST API
 - RMM
 - Open API
 - API Key

description: Learn about the concepts of REST API!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->

## REST API
웹 어플리케이션에서는 `HTTP 메서드`를 이용해 서버와 통신한다.  
이런 사용은 아무런 규칙 없이 이루어지는 것이 아니다.  
요청과 응답을 할 때, '제대로 보내고 받을 수 있는' 일종의 규약이 존재한다.  
`REST`는 `Representational State Transfer`의 아니셜로,  
`Roy Fielding`의 박사 학위 논문에서 웹(`http`)의 장점을 최대한 활용할 수 있는 아키텍처로써 처음 소개되었다.  
`REST API`는 *웹에서 사용되는 데이터나 자원(Resource)을 HTTP URI로 표현하고, HTTP 프로토콜을 통해 요청과 응답을 정의하는 방식*을 말한다.  

---  

### RMM
`REST API`를 작성할 때에는 몇 가지 지켜야할 규칙들이 있다.  
`Roy Fielding`이 논문에서 제시한 REST 방법론을 보다 더 실용적으로 적용하기 위해,  
`Leonard Richardson`은 `REST API`를 잘 적용하기 위한 4단계 모델을 만들었다.  
![Richardson 성숙도 모델 (RMM)](/assets/img/rmm.png)  

REST 성숙도 모델은 총 4단계 (0~3단계)로 나누어진다.  
앞서 이야기한 `Roy Fielding`은 이 모델의 모든 단계를 충족해야 `REST API`라고 부를 수 있다고 주장했다.  
그러나 실제로 엄밀하게 3단계까지 지키기 어렵기 때문에 2단계까지만 적용해도 좋은 API 디자인이라 볼 수 있다  
이런 경우 `HTTP API`라고도 부른다.  

---  

#### REST 성숙도 모델 - 0단계
0단계에서는 `단순히 HTTP 프로토콜을 사용`하기만 해도 된다.  
이 경우, 해당 `API`를 `REST API`라고 할 수는 없으며, 0단계는 좋은 `REST API`를 작성하기 위한 기본 단계이다.  
![0단계](/assets/img/0stage.png)  

---  

#### REST 성숙도 모델 - 1단계
REST 성숙도 모델에 따르면, 1단계에서는 `개별 리소스와의 통신을 준수`해야한다.  
`REST API`는 웹에서 사용되는 모든 데이터나 자원(Resource)을 `HTTP URI`로 표현하기 때문에,  
모든 자원은 개별 리소스에 맞는 `엔드포인트(Endpoint)`를 사용해야하고,  
요청하고 받은 자원에 대한 정보를 응답으로 전달해야한다.  
앞선 0단계에서는 모든 요청에서 `엔드포인트`로 `/appointment`를 사용했다.  
하지만 1단계에서는 요청하는 리소스가 무엇인지에 따라 각기 다른 엔드포인트로 구분하여 사용해야 한다.  

![1단계](/assets/img/1stage.png)  

예시와 같이, 어떤 리소스를 변화시키는지 혹은 어떤 응답이 제공되는지에 따라 각기 `다른 엔드포인트`를 사용하기 때문에,  
적절한 엔드포인트를 작성하는 것이 중요하다.  
엔드포인트 작성 시에는 동사, HTTP 메서드, 혹은 어떤 행위에 대한 단어 사용은 지양하고,  
리소스에 집중해 명사 형태의 단어로 작성하는 것이 바람직한 방법이다.  

---  

#### REST 성숙도 모델 - 2단계
REST 성숙도 모델 2단계에서는 `CRUD`에 맞게 적절한 HTTP 메서드를 사용하는 것에 중점을 둔다.  
앞선 0,1단계에서는 모든 요청을 `CRUD`에 상관없이 `POST`로 하고 있다.  
그러나 REST 성숙도 모델에 2단계에 따르면, 이는 `CRUD`에 따른 적합한 메서드를 사용한 것은 아니다.  
![2단계](/assets/img/2stage.png)  

응답코드 또한 고려하여 재작성하면 다음과 같다.  
![2단계_수정](/assets/img/2stage-mod.png)  

메서드를 사용할 때의 규칙은 다음과 같다.  
- `GET` : 서버의 데이터를 변화시키지 않는 요청
- `POST` : 요청마다 새로운 리소스를 생성한다. 
- `PUT` : 요청마다 같은 리소스를 반환한다.  
> 매 요청마다 같은 리소스를 반환하는 특징을 멱동([idempotent](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent))하다고 한다.  
> 멱등성을 갖는 `PUT`과 `POST`는 구분하여 사용해야 한다.  
- `PUT` : 데이터 전체를 교체한다.  
- `PATCH` : 데이터의 일부를 수정한다.  
더 자세한 내용은 [여기](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)를 확인하자.  

`API`를 작성할 때, `REST` 성숙도 모델의 2단계까지 적용을 하면, 대체로 잘 작성된 API라고 여긴다.  
물론 `Roy Fielding`은 3단계까지 만족하지 못한다면 `REST API`가 아니기 때문에 `HTTP API`라고 불러야 한다고 주장하지만,  
**모범적인 API 디자인 조차도 REST 성숙도 모델의 3단계까지 적용한 경우는 극히 드물다.**  
따라서 3단계까지 무조건 모두 적용해야 한다는 것은 아니다.  

---  

#### REST 성숙도 모델 - 3단계
마지막 단계는 `HATEOAS`(Hypertext As The Engine Of Application State)로 표현되는 `하이퍼미디어 컨트롤`을 적용한다.  
3단계의 요청은 2단계와 동일하지만, 응답에는 리소스의 `URI를 포함한 링크 요소`를 삽입하여 작성한다는 것이 다르다.  
이때 응답에 들어가게 되는 링크 요소는 응답받은 다음에 할 수 있는 다양한 액션들을 위해 많은 하이퍼미디어 컨트롤을 포함한다.  
![3단계](/assets/img/3stage.png)  

위처럼 어떤 값을 조회 한 후에, 그 시간대에 예약할 수 있는 링크를 삽입하는 등,  
새로운 기능에 접근할 수 있도록 하는 것이 3단계의 특징이다.  

---

### Reference
- [5가지 기본적인 REST API 디자인 가이드](https://blog.restcase.com/5-basic-rest-api-design-guidelines/)
- [호주 정부 API 작성 가이드](https://api.gov.au/sections/getting-started.html)
- [구글 API 작성 가이드](https://cloud.google.com/apis/design?hl=ko)
- [MS의 REST API 가이드 라인 Github](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md)
- [MS의 RESTful 웹 API 디자인 아티클](https://learn.microsoft.com/ko-kr/azure/architecture/best-practices/api-design)  
- [MDN HTTP 요청 메서드](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)  

---

### Open API
`Open API`는 누구에게나 열려있는 API이다.  
하지만 무제한으로 이용할 수 있지는 않고, 기관이나 API마다 정해진 이용 수칙이 있다.  

---

### API Key
API를 이용하기 위해서는 `API Key`가 필요하다.  
`API Key`는 서버의 문을 여는 열쇠라고 생각할 수 있다.  
클라이언트의 요청에 따라 서버에서 응답한다는 말은, 서버를 운용하는 데에 비용이 발생한다는 말이다.  
따라서 서버 입장에서 아무런 조건 없이 익명의 클라이언트에게 데이터를 제공할 의무도, 이유도 없다.  
(가끔 API Key가 필요하지 않은 경우도 있다.)  
그래서 로그인된 이용자에게만 자원에 접근할 수 있는 권한을 API Key의 형태로 제공하고,  
데이터를 요청할 때 API Key를 같이 전달해야만, 원하는 응답을 받을 수 있다.  

