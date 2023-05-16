---
title: Digital Signature
tags: 
 - public key
 - private key
 - hashing
 - verification

description: Learn about the concept of Digital Signature!
---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

# Digital Signature
우리가 수기로 작성하는 일반적인 서명을 통해 해당 문서에 대해  
"`나`라는 사람이 읽었으며, 문서에 문제가 없음을 확인했고, 문서의 내용에 동의함”을 표현할 수 있다.  
즉, 서명의 역할은 문서의 진위성과 무결성을 보증하는 것이다.  
<br>
그렇다면 디지털화된 데이터에 대해서는 어떻게 진위성과 무결성을 보장할 수 있을까?  
디지털화된 데이터를 네트워크를 통해 전달하는 과정에서 훼손되거나 탈취되어 변조될 가능성도 있고,  
정상적인 사용자가 아닌 악의적인 해커가 사용자인 척 데이터를 전달할 수도 있다.  
<br>
**디지털 서명(Digital Signature)**은 수학적 메커니즘을 통해 데이터의 진위성과 무결성을 검증한다.  
디지털 서명은 `개인 키`를 사용해 원본 데이터에 서명을 한 서명 데이터를 의미한다.  
<br>
개인키를 사용하여 서명의 주체가 정상적인 사용자인 ‘나’라는 것을 인증하고,  
이 데이터가 올바른 데이터가 맞다고 증명하는 것이다.  
디지털 서명된 데이터를 받는 수신자는 공개키로 디지털 서명을 복호화하여 진위여부를 확인할 수 있다.
<br>
이를 통해 수신자는 네트워크를 통해 데이터가 도착하기까지 변조되었는지 확인할 수 있을뿐더러,  
악의적인 사용자의 사칭 유무 역시도 확인할 수 있다.  
<br>
이러한 장점으로 인해 오늘날 디지털 서명은 전자 문서, 거래, 메시지에 대한 출처, 신원 및 상태에 대한 보증의 용도로 폭넓게 사용되고 있다.  

---

## Background
공개키 암호화 방식은 공개키와 개인키로 구성된 한 쌍의 키를 사용한 암호화 방식이다.  
두 키는 타원곡선 알고리즘(Elliptic Curve Algorithm, ECC)을 사용하여 생성된다.  
공개키로 암호화된 데이터는 해당 개인키로 복호화할 수 있다.  
따라서 공개키는 외부에 공개하고, 개인키는 기밀로 유지해야 한다.  

![public-key](../../assets/img/public-key.png)  


![public-key-encryption](../../assets/img/public-key-encryption.gif)  

공개키로 암호화된 데이터는 암호화한 사용자(개인키 소유자)만이 복호화할 수 있다.  
만약 암호화된 데이터를 다른 사람에게 보내야 하는 경우,  
해당 사용자의 공개키로 데이터를 암호화하고, 수신자는 송신자의 개인키로 복호화해야 한다.  
이 방식을 사용하면 중요한 데이터를 암호화하여 승인된 사용자에게만 전달할 수 있다.

![private-key](../../assets/img/private-key.png)  


![private-key-encryption](../../assets/img/private-key-encryption.gif)


반대로 개인키로 암호화된 데이터를 공개키로 해독하는 방식도 있다.  
이러한 방법은 중요한 데이터를 암호화하는 데에는 적합하지 않다.  
<br>
공개키는 누구에게나 공개되어 있기 때문에 누구나 쉽게 복호화를 할 수 있다.  
따라서 데이터의 내용을 숨기는 것이 아니라, 디지털 서명을 하여,  
데이터의 무결성과 진위성을 검증해야 할 때는 개인키로 암호화하는 방식을 사용한다.

---

## How does it work
디지털 서명은 크게 세 단계로 나뉜다.  

1. 해싱
2. 서명
3. 검증

![digital-signature](../../assets/img/digital-signature.png)  

---

### Hashing
원본 데이터를 해싱한다.  
원본 데이터의 크기는 제각기 다를 수 있지만, 해싱되었을 때는 동일한 길이의 해시값을 가지게 된다.  

> 원본 데이터를 해싱하는 것은 필수적인 것은 아니다.  
> 해싱하지 않은 원본 데이터에 개인키로 서명을 할 수도 있기 때문이다.  
> 그러나 해싱함으로써 고정된 길이의 값을 비교하는 것이 무결성을 검증하는데 훨씬 간편하기 때문에 사용한다.

---

### Signature
비대칭키 암호화 방식을 사용해 해싱된 데이터에 서명한다.  
서명하는 방식은 다양하지만, 일반적으로 송신자의 개인키로 해시값을 암호화한다.  
이 암호화된 결과값이 바로 디지털 서명이다.  
<br>
디지털 서명은 개인키로 암호화되었기 때문에 공개키로 복호화할 수 있으며,  
정상적으로 복호화될 경우 원본 데이터의 해시값이 나오게 된다.  
<br>
서명이 완료되면 송신자는 `원본 데이터`와 `디지털 서명`, `송신자의 공개키`를 함께 전송한다.  

---

### Verification
수신자는 `송신자의 공개키`를 가지고 `디지털 서명을 복호화`한다.  
검증 과정에서는 두 데이터를 비교한다.  

- 디지털 서명이 송신자의 개인키에 의해 암호화되었다면, 원본 데이터의 해시값이 나올 것이다.  
- 또한, 수신자는 원본 데이터를 해싱하여 데이터의 해시값을 구한다.  

이 두 해시값을 비교하여 만약 해시값이 동일하다면, 데이터가 정상적으로 송신자에 의해 서명된 것임을 확인할 수 있다.  

![digital-signature-flow](../../assets/img/digital-signature-flow.png)  

---

## Features
디지털 서명은 세 가지 특징을 갖고 있다.  

- **데이터 무결성**  
수신자는 메시지가 전송되는 동안 위변조가 일어나지 않았음을 검증할 수 있다.  
만약 송신자의 공개키로 디지털 서명을 복호화한 값이 원본 데이터를 해싱한 값과 다른 경우,  
해당 송신자의 개인키로 암호화된 서명이 아니거나, 원본 데이터가 훼손되었을 수 있다.

- **진위성**  
송신자의 개인키가 안전하게 보관되었다는 전제하에,  
수신자는 디지털 서명이 송신자에 의해 생성되었음을 확인할 수 있다.  

- **부인 방지**  
송신자의 개인키가 안전하게 보관되었다는 전제하에,  
서명이 생성되고 나면, 이 서명이 송신자에 의해 서명되었다는 사실을 부정할 수 없다.  

## Prerequisites
디지털 서명 시스템은 다음의 세 가지 요소를 필수적으로 갖추어야 합니다.

- **알고리즘**  
디지털 서명 체계에서 사용되는 알고리즘은 수준이 중요합니다.  
신뢰할 수 있고, 널리 사용되어 그 안전성이 입증된 해시 함수와 암호화 알고리즘을 사용해야 한다.  

- **구현**  
디지털 서명 방식은 데이터의 무결성 및 진위성과 직결되기 때문에 결점 없는 시스템을 구현하는 것 역시 중요하다.  

- **개인키**  
개인키가 유출되거나 손상될 경우, 진위성과 부인 방지 속성이 무효화된다.  
특히 암호화폐에서 개인키를 잃어버릴 경우 재정적 손실로 이어지기도 한다.  

블록체인에서 디지털 서명은 송금을 위해 트랜잭션을 생성하여 서명하고 승인하는 데 사용된다.  
특히 지갑(월렛) 방식을 사용하는 암호화폐는 개인키를 소유한 사람만이 코인을 사용할 수 있기 때문에,  
개인키를 안전하게 보호하는 것이 중요하다.  