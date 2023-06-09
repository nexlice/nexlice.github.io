---
title: Hash Function
tags: 
 - anonymity
 - integrity
 - collision
 - preimage

description: Learn about the concept of Hash Function!
---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

# Hash Function _

---

## Hashing
**해싱(Hashing)** 은 다양한 크기의 입력값을 고정된 크기의 출력값으로 생성해 내는 과정을 의미한다.  

---

## Etymology
해시(Hash)의 어원은 고기와 감자를 잘게 다져서 섞어 만든 요리이다.  
~~예시로 해시 포테이토라는 요리도, 감자를 잘게 다져서 튀긴 음식이다.~~  
어원이 이렇듯, 해시 함수도 원본 데이터를 잘게 조각내어 원본을 알아볼 수 없게 만든다.  

---

## Hash Function
지금까지 배운 암호화는 암호화와 복호화가 한 세트인, ‘원본 보존이 가능한’ 암호화였다.  
그러나 해시 함수는 한번 해싱했다면, 그 해싱된 값을 통해 입력값을 유추할 수 없다.  
이러한 특성 때문에, 해시 함수를 단방향 암호라고 부른다.  

해시 함수는 다음 중요한 특징을 가진다.

1. 해시 함수는 어떠한 크기의 입력이 들어와도 동일한 크기의 출력값을 반환한다.  
2. 해시 함수는 서로 다른 입력값에 대해 완전히 다른 출력값을 반환한다.  
3. 해시 함수는 출력값을 통해 입력값을 유추할 수 없다.  

![hash-function](../../assets/img/hash-function.png)  

오늘날에는 여러 종류의 해시 함수가 존재하며,  
그 중 암호 해시 함수는, 블록체인 및 다양한 분산 시스템에 데이터 무결성과 보안을 보장하는 데 사용된다.  

---

## How does it work
해시 함수는 **다양한 크기의 입력값을 사용해 고정된 크기의 출력값을 생성**한다.  
가령 `SHA-256` 알고리즘은 어떤 입력값을 넣어도 256비트 길이의 값을 출력하며,  
SHA-1은 160비트 길이의 값을 출력한다.  

![sha-1](../../assets/img/sha-1.png)  

---

## In Blockchain
기존의 해싱은 데이터베이스 조회, 파일 분석, 데이터 관리 등에 사용되어 왔다.  
반면, 암호 해시 함수는 메시지 인증, 디지털 서명 등 보안 애플리케이션에서 사용될 수 있다.  
<br>
특히, 암호화폐 프로토콜에서 중요한 기술 중 하나로,  
사용자에게 익명성을 보장하고, 트랜잭션을 하나로 연결 및 압축하며, 블록을 연결하는 동시에 그 무결성을 보장하는 역할을 한다.  

---

## Anonymity  
공개키를 해싱한 값을 지갑 주소로 사용하여 거래를 익명화할 수 있다.
트랜잭션 기록에는 해시값으로 암호화된 지갑 주소와 송금 및 잔액을 확인할 수 있을 뿐,  
해당 지갑의 주인이 누구인지 파악할 수는 없다.

---

## Integrity
![hash-compare](../../assets/img/hash-compare.png)  
입력값이 조금이라도 다르면 출력값이 변하는 해시 함수의 특성을 이용하여 블록체인에서 무결성을 검증하는 경우,  

```bash
1. 블록의 헤더에 있는 `이전 블록 해시` 는 `이전 블록의 값을 해싱한 값`을 사용해 이전 블록을 가리킨다.  
만약 이전 블록을 해싱한 값이 달라진 경우, 해당 블록 또는 가리키고 있던 이전 블록에 위변조가 일어났음을 알 수 있다.
2. 블록에 저장된 모든 트랜잭션을 머클트리 알고리즘을 사용해 하나의 해시값으로 저장하여 `머클루트`를 만든다.  
만약 트랜잭션이 하나라도 변한 경우, 머클루트의 값이 변했다는 것을 통해 위변조가 일어났음을 알 수 있다.
3. 입력값을 일정한 길이의 값으로 축약해 주는 특성을 사용하여 대용량 파일의 문서를 해싱한 뒤, 해싱된 값만 비교하여 위변조가 일어났음을 알 수 있다.
```
이러한 방식은 모든 데이터를 대조할 필요 없이, 고정된 크기의 해시값을 비교하면 되기 때문에,  
많은 양의 데이터를 저장하거나 기억할 필요 없이 무결성을 검증할 수 있다.  

---

## Determining Mining Node
해시값을 사용해 채굴 노드를 정할 수도 있다.  
최초의 블록체인 암호화폐인 비트코인에서는 PoW(작업 증명) 방식을 사용해 어떤 노드가 블록을 만들지 정한다.  
작업 증명 방식에서는 특정 조건을 만족하는 해시값을 만족하기 위해 입력값인 논스(Nonce)를 찾아야 한다.  
이를 가장 먼저 찾는 노드에게 블록을 채굴할 권한을 주며 채굴에 대한 보상으로 비트코인을 제공한다.  

---

## Security
블록체인에서 사용되는 해시 함수는 단방향 알고리즘을 사용하고, 입력값이 조금만 달라져도 아예 다른 형태로 변하기 때문에,  
해싱된 값을 이용하여 기존의 값을 찾기란 매우 어렵다.  
그렇기에 일반적으로 암호 해시 함수를 복호화하기 위해서는 수많은 무차별 대입을 시도해야 한다.  
<br>
그러나 이러한 해시 함수에도 약점은 있다.  
해시 함수의 특징 중 하나인 ‘항상 고정된 길이의 출력값‘때문에 한 가지 문제점이 발생한다.  
서로 다른 입력값을 해시 함수에 넣었는데 **동일한 출력값을 내뱉는 경우**이다.  
<br>
이를 `해시 충돌`이라 한다.  
해시 충돌은 시스템에 심각한 위협이 될 수 있기 때문에 충돌을 피하는 것은 해시함수를 만들 때 중요한 요소 중 하나이다.  
<br>
이러한 점들을 고려하여 암호 해시 함수의 안전성은 다음의 세 가지 요소로 평가할 수 있습니다.

- Collision Resistance : 충돌 저항성
- Preimage Resistance : 역상 저항성
- Second Preimage Resistance : 제2 역상 저항성

---

### Collision Resistance
앞서 설명했듯이, 서로 다른 입력값이 동일한 출력값을 갖게 되는 것을 충돌이라고 했다.  
충돌 저항성은 어떤 해시 함수가 충돌하는 서로 다른 두 입력값을 가졌는지 발견되지 않은 상태를 의미한다.  
<br>
이는 마치 사람의 지문과 같다.  
지문은 완전히 같을 확률이 매우 적기 때문에, 사람을 식별할 때 주민등록번호를 일일이 입력하는 대신 지문을 사용할 수 있다.  
<br>
사실상 해시 함수의 입력값은 그 길이와 종류가 무한하지만,  
출력값은 유한하기 때문에 누군가가 충돌하는 두 입력값을 발견할 가능성도 있다.  
<br>
그러나 해시 함수의 충돌을 발견할 가능성은 매우 적다.  
가령 `SHA-256`의 출력값의 각 자리에는 0~9, a~f 사이의 16진수가 하나 들어가며,  
총길이는 64자리로, 비트로 환산하면 256비트가 되며, 경우의 수는 2^256이 된다.  
<br>
2^256은 10^78와 근사한 수치이다.  
우주의 모든 원자의 개수가 10^80개라는 것을 감안하면 사실상 SHA-256의 충돌을 찾는 것은 불가능에 가깝다.  
따라서 충돌이 없는 해시 함수는 존재하지 않지만, 충돌 저항성이 있다고 간주하는 해시 함수는 존재한다.  
<br>
이론적으로 양자 컴퓨터를 사용하게 된다면,  
계산 성능을 획기적으로 늘리는 것이 가능하기 때문에 2^256개의 가능성을 일일이 대입하는 것이 어렵지 않을 것이다.  
~~그러나 양자 컴퓨터가 어느 순간 갑자기 보편화될 가능성은 적기 때문에 지금 당장 걱정할 필요는 없다.~~  

---

### Preimage Resistance
역상 저항성은 어떤 해시 함수가 특정한 값을 출력하는 입력값을 찾을 확률이 매우 낮을 경우를 의미한다.  
이는 단방향 함수의 성질과 연관된다.  
단방향 함수는 입력값을 통해 출력값을 얻을 수는 있지만, 출력값을 통해 입력값을 얻을 수는 없는 함수이다.  
<br>
역상 저항성은 데이터를 보호하는 데 매우 유리하다.  
메시지의 해시값을 사용하면 해당 메시지의 원본을 공개하지 않고도 진위성을 검증할 수 있기 때문이다.  
<br>
실제로 패스워드에 대한 진위성을 검증할 때도,  
패스워드 원문을 비교하지 않고, 패스워드를 해싱한 값을 사용하여 패스워드가 노출되는 것을 방지한다.  

---

### Second Preimage Resistance
제2 역상 저항성은 충돌 저항성과 역상 저항성이 복합적으로 작용한 경우로,  
`A`라는 입력값의 해시값과 동일한 해시값을 내는 `B` 입력값을 누군가가 알고 있지 않은 경우이다.  
반대로 이 `B` 입력값을 누군가가 발견한 경우 제2 역상 공격이 가능하다.  
<br>
충돌 가능성은 동일한 해시값을 가진 서로 다른 두 입력값을 찾는 것이지만,  
제2 역상 공격은 `A` 입력값을 통해 `A'`라는 해시값이 나왔을 때,  
`A'` 해시값을 출력하게 만드는 B 입력값을 찾는 것이다.  
따라서 제2 역상 저항성은 충돌 저항성이 전제되어야 한다.