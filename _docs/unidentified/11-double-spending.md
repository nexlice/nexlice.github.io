# Double Spending
**이중 지불(Double Spending)**이란,  
디지털 현금 시스템 내에 동일한 하나의 자산이 두 명의 수신자에게 동시에 전송되는 문제를 의미한다.  
<br>
가령 A가 자신의 계좌에 있는 2,000원을 B에게 보내는데,  
해당 송금이 처리되기 전 A가 다시 아직 자신의 계좌에 있는 2,000원을, C에게 송금하도록 요청한다고 생각해 보자.  
A가 자신의‘2,000원ʼ이라는 자산 데이터를 복제하여 B에게도 보내고 C에게도 보낸 것이다.  
<br>
정상적인 상황이라면 A가 B에게 보내는 송금이 먼저 처리되어, C에게 보내는 송금은 완료되지 않을
것이다.  
그러나 디지털 시스템의 허점으로 인해 C에게 보내는 송금도 처리가 될 수도 있다.  
<br>
디지털 금융 시스템에서는 특정 자산이 복제될 수 없게 하는 것이 가장 중요하다.  
A가 자신의 자산을 열번 복제하여 2,000원을 20,000원으로 만든다면 해당 금융 시스템 자체가 붕괴할 것이다.  
<br>
디지털 자산의 복제를 막는 것은 어려운 문제이지만,  
이러한 문제를 방지할 수 있어야 디지털 현금 시스템을 사용할 수 있다.  
오늘날 이중 지불 문제를 방지하기 위한 다양한 방법이 제시되고 있다.

---

## Solutions

---

### Centralized Approach
중앙화된 방법은 탈중앙화된 방법에 비해 간단하다.  
일반적인 시스템에는 해당 시스템을 관리하는 감독이 있으며, 감독은 자산의 발행과 분배를 관장한다.  
이중 지불 문제를 해결하는 중앙화된 접근법의 대표적인 예시로는 데이비드 차움(David Chaum)의 `eCash`가 있다.  

----

#### eCash
암호학자 데이비드 차움은 자신의 논문 'Blind Signatures for Untraceable Payments'에서 은행이
고객에게 익명성을 보장하고 PP 교환이 가능한 디지털 자산을 발행하기 위한 방식으로 **은닉 서명(Blind
Signature)**을 제안하였다.  

> **은닉 서명(Blind Signature)이란?**  
> 암호학에서 메시지의 내용이 서명되기 전에 은닉(블라인드)되는 디지털 서명의 한 형태이다.  
> 은닉 서명은 일반적인 디지털 서명 방식처럼,  
> 은닉되기 전의 원본 메시지로 공개적으로 검증될 수 있다. 
> <br>
> 이는 서명자와 메시지 작성자가 일치하지 않는 프라이버시가 보장되어야 하는 프로토콜에서 일반적으로 사용된다.  
> 예로는 암호화 선거 시스템과 디지털 현금제도가 있다.

eCash의 동작 방식은 다음과 같다.  
**Case 1: 사용자가 자신의 계좌에 있는 달러를 디지털 현금으로 바꾸고 싶은 경우**  
1. 사용자는 먼저 자신의 계좌에 있는 달러를 디지털 현금으로 바꾸고 싶다고 은행에 알린다.  
2. 은행은 사용자의 계좌에 잔액이 있는지 확인하고, 하나 또는 여러 개의 **임의의 숫자**를 생성한다.  
    - 만약 사용자가 다섯 개의 숫자를 생성했다면, 각 숫자는 20달러에 해당한다.  
    (사용자가 두 개의 숫자를 생성했다면 각 숫자는 달러에 해당한다.)  
    - 이 숫자는 디지털 현금 지폐처럼 사용된다.  
    사용자는 은행이 자신의 숫자를 추적할 수 없도록 각 숫자에 은닉 요소(Blinding Factor)를 추가한다.  
3. 이후 사용자는 은닉 요소를 추가한 숫자 데이터를 은행에 넘겨준다.  
4. 은행은 사용자의 계좌에서 달러를 인출하고, 5개의 데이터로 각각 달러씩 교환할 수 있음을 증명하는 메시지에 서명한다.  
5. 사용자는 이제 은행에서 발행된 자금을 사용할 수 있다.  

**Case 2: 디지털 현금으로 결제하고 싶은 경우**  
1. 사용자가 레스토랑에서 달러짜리 메뉴를 먹는 경우,  
사용자는 자신의 숫자 중 음식값을 지불하기 위한 숫자 두 개의 은닉 요소를 제거하여 레스토랑 주인에게 건네준다.  
2. 레스토랑 주인은 사용자가 다른 상점에서 이 숫자 두 개를 다시 사용하는 것을 방지하기 위해, 이를 즉시 은행에 청구한다.  
    - eCash를 그대로 가지고 있으면, 사용자가 다른 곳에서 이 달러를 또 사용할 수 있기 때문이다.  
3. 은행은 레스토랑 주인이 제시한 숫자에 있는 서명이 유효한지 확인하고, 정확하다면 레스토랑
주인에게 달러를 입금한다.  
4. 사용된 숫자는 소각된다.  

차움의 eCash는 비밀 송금에 유용하다.  
디지털 현금은 기본적으로 숫자로 구성되며, 은행에서 서명을 하므로 당사자들의 신원을 확인할 필요가 없기 때문이다.  
<br>
그러나 은행 자체가 단일 장애 지점이기 때문에, 은행에 문제가 생길 경우, 결제 시스템 전체에 문제가 생길 수 있다.  
발행된 숫자, 즉 지폐는 그 자체로는 아무런 의미도 없으나, 은행이 그 가치를 부여하고 보증하기 때문이다.  
<br>
eCash에서 고객은 은행의 통제 아래에 있으며, 돈을 사용하기 위해서는 은행의 허가를 받아야 한다.  
이것이 바로 암호화폐가 해결하고자 하는 문제이다.  

---

### Decentralizaed Approach
은행과 같은 중앙화된 감독이 없는 생태계에서 이중 지불을 방지하는 것은 더욱 어렵다.  
따라서 균등한 힘을 가진 참여자들이 서로 부정행위를 방지하고 정직하게 행동할 수 있도록 장려하기 위해,  
일련의 규칙을 마련하고 협력해야 한다.  
<br>
이중 지불 문제에 대한 가장 혁신적인 해결책은 비트코인 백서에서 확인할 수 있다.  
비록 직접적으로 그 이름을 언급하지는 않았지만,  
사토시 나카모토가 제시한 데이터 구조는 오늘날 **블록체인**이라는 이름으로 잘 알려져 있다.  
<br>
블록체인은 몇 가지 특별한 속성을 가진 데이터베이스이다.  
<br>
비트코인 코어, geth 등 특정 소프트웨어를 실행하면 누구든지 블록체인 네트워크에 참여할 수 있다.  
이렇게 소프트웨어를 실행하여 네트워크에 연결된 컴퓨터를 노드라고 한다.  
네트워크에 참여한 모든 노드는 블록체인의 데이터베이스 사본을 다운로드하고, 다른 노드들과 동기화할 수 있다.  
<br>
퍼블릭 블록체인의 경우, 누구나 언제든지 네트워크에 참여하여,  
제네시스 블록부터 최신블록까지 모든 트랜잭션을 확인할 수 있기 때문에,  
이중 지불을 시도하는 부정 트랜잭션을 감지할 수 있다.  
<br>
사용자가 트랜잭션을 전송하면 이는 바로 블록체인에 추가되지 않고, 채굴을 통해 먼저 하나의 블록에 포함되어야 한다.  
따라서 트랜잭션은 생성되었을 때가 아니라,  
트랜잭션이 포함된 블록이 체인에 추가되었을 때 유효하다고 간주한다.  
그렇지 않으면, 송신자가 하나의 코인으로 여러 트랜잭션을 생성하여 이중지불 문제를 발생시킬 수 있다.  
<br>
트랜잭션이 체인에 올라가 확정되면 새로운 사용자에게 소유권이 할당되기 때문에 코인은 이중지불 될 수 없다.  
이러한 이유로 트랜잭션을 유효한 것으로 간주하기 전에, 많은 이들이 복수의 승인을 기다릴 것을 추천한다.  
체인으로 이어진 각 블록을 수정하는 데에는 엄청난 노력이 필요하기 때문이다.  
<br>
레스토랑 예시로 돌아가 보자.  
이 레스토랑은 이번 주부터 비트코인으로도 결제를 할 수 있다고 하자.  
김코딩은 지난번에 먹었던 메뉴를 다시 주문한다.  
가격은 0.005BTC이다.  
1. 레스토랑 주인은 김코딩에게 음식값을 지불할 비트코인 주소를 알려준다.  
2. 김코딩은 자신의 소유였던 0.005BTC가 레스토랑 주인의 소유라고 주장하는 내용과,  
이를 서명한 트랜잭션을 생성하고, 네트워크의 다른 노드들에게 전송한다.  
3. 서명된 트랜잭션을 통해 네트워크에 연결된 모든 노드는 트랜잭션을 자세하게 뜯어보지 않아도,  
김코딩의 서명을 통해 김코딩이 실제로 해당 0.005BTC의 소유자였으며,  
이를 송금할 권한이 있음을 검증할 수 있다.

그러나 트랜잭션은 체인에 블록이 올라가야 유효하다.  
트랜잭션이 블록에 올라가고, 블록이 체인에 연결되어야 실제로 송금이 완료된 것이다.  
<br>
만약 체인에 올라가지 않은 블록에 기록된 트랜잭션을 수용한다면,  
이는 eCash에서 달러를 은행에 청구하지 않고 그대로 가지고 있는 것과 같다.  
트랜잭션이 블록에 올라가 체인에 연결되지 않은 경우,  
다른 노드들은 이 트랜잭션이 처리되지 않은 것으로 판단하기 때문에,  
김코딩이 0.005BTC를 가지고 있는 것이나 마찬가지이다.  
<br>
**블록이 체인에 연결되더라도, 트랜잭션이 완전히 처리된 것은 아니다.**  
<br>
실제로 블록에 있는 트랜잭션이 수정이 불가능하다고 판단되어 온전히 완료되는 시점은,  
블록이 체인에 올라가고 자신의 뒤에 블록이 일정 개수 이상 연결된 시점이다.  
이를 컨펌 횟수라고 한다.  
<br>
블록이 체인에 올라가더라도, 만약 체인이 두 갈래로 갈라진 상태에서 블록이 추가되었다면,  
체인 재구성이 일어나 해당 블록이 고아 블록이 되어 트랜잭션이 취소될 수도 있기 때문이다.  
<br>
비트코인에서는 특정 블록 뒤에 6개의 블록이 더 쌓여야 안전하다고 본다.  
블록이 하나 생성될 때 10분이 소요되기 때문에,  
트랜잭션이 완료되는 시점은 블록이 체인에 올라간 후 약 1시간이 지난 후이다.  
<br>
이렇듯 여러 번 확증되어 거래의 완결 정도가 높아지는 것을 Probabilistic finality(확률적 완결성)라고
한다.  

---

## Bitcoin Double Spending
비트코인의 기본 프로토콜은 이중 지불 공격을 방어할 수 있도록 세심하게 설계되어 있다.  
즉, 송신자를 포함한 그 누구도 체인에 올라간 트랜잭션을 되돌릴 수 없다.  
이를 되돌리기 위해서는 해당 블록과, 해당 블록 이후에 생성된 블록들을 되돌려야 하는데,  
이는 비현실적인 수준의 연산 능력이 필요하기 때문이다.  
<br>
그러나 트랜잭션을 **승인하는 노드를 겨냥한 소규모 이중 지불 공격**도 존재한다.  
<br>
예를 들어, 바쁜 패스트푸드점에서는 트랜잭션이 블록에 포함되기까지 기다리고 싶어 하지 않을 것이다.  
만약 패스트푸드점에서 **즉각적인** 결제, 즉 블록이 체인에 올라간 시점이 아니라,  
트랜잭션이 생성된 시점을 결제 시점으로 수용한다면, 이중 지불 공격에 노출될 수 있습니다.  
<br>
누군가가 햄버거를 주문하고, 트랜잭션을 생성해 금액을 지불하고, 동일한 금액을 자신의 다른 주소로 전송할 수 있다.  
만약 자신의 다른 주소로 전송한 트랜잭션의 수수료가 더 높으면,  
이 트랜잭션이 먼저 승인될 수도 있으며, 이전에 패스트푸드점에서 생성한 트랜잭션은 무효화될 것이다.  
<br>
이중 지불을 수반한 세 가지 공격 방법들이 있습니다.  
1. **51% 공격**  
단일 주체나 조직이 51% 이상의 해시 레이트를 가지게 될 경우,  
이들은 원치 않는 트랜잭션을 배제하거나 트랜잭션 순서를 조작할 수 있게 된다.  
비트코인에서 해당 공격이 발생할 가능성은 매우 낮지만, 규모가 작은 다른 네트워크에서는 발생할 수도 있다.  
2. **레이스 공격(Race Attacks)**  
동일한 자금을 사용하는 두 개의 충돌하는 트랜잭션이 연속으로 전송되지만, 하나의 트랜잭션만
승인되는 것이다.  
해당 공격의 목표는 앞의 패스트푸드점 예시처럼 두 개의 충돌하는 트랜잭션 중,  
자신에게 이익이 되는 트랜잭션만 유효하게 만들어 결제를 무효화하는 것이다.  
레이스 공격은 수신자가 체인에 올라가지 않은 트랜잭션을 결제로 수용할 때 가능하다.  
3. **핀니 공격(Finney Attacks)**  
공격자는 네트워크에 즉각적으로 트랜잭션을 전송하지 않고,  
코인을 자신의 다른 지갑으로 전송하는 트랜잭션을 미리 생성해 두고,  
블록을 미리 채굴해 두어 해당 블록에 기록한다.  
<br>
동일 코인을 다른 트랜잭션에서 사용하는 대신, 이전에 채굴한 블록만을 전송하며, 결제는 무효화된다.  
핀니 공격은 특정한 순서에 따라 사건이 발생해야 하며,  
수신자는 체인에 올라가지 않은 트랜잭션을 수용해야 발생할 수 있다.  

이중 지불은 디지털 현금 시스템에서 경제적 이익을 얻기 위해 동일한 자금을 여러 번 사용하는 것이다.  
이중 지불 문제는 적절한 해결책이 없었기 때문에, 디지털 현금 시스템의 발전에 큰 걸림돌이 되어
왔다.  
<br>
그러나 다행히도, 은닉 서명이 중앙화된 경제 체계에 해결책을 제시했다.  
또한 작업 증명 메커니즘과 블록체인 기술의 개발로 탈중앙화된 자산의 형태인 비트코인이 탄생했으며,  
비트코인은 수천 개의 암호화폐 프로젝트에 영감을 주었다.  
<br>
이러한 기존 시스템과의 차이로 인해, 블록체인에 대한 공격 방식도 기존의 데이터베이스 공격 방식과는
다르다.  
따라서 블록체인 공격 방식을 미리 알아두고 예방하는 것이 중요하다.