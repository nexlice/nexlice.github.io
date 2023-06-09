#  51 Precent Attack
51% 공격을 이해하기 위해서는 채굴과 블록체인 시스템에 대한 이해가 필요하다.  
비트코인의 주요한 강점이자 블록체인 기술의 근간을 이루는 특징은, 데이터를 구축하고 검증하는 분산성이다.  
<br>
탈중앙화 방식은 노드들이 프로토콜 규칙을 준수하고, 모든 네트워크 참여자가 블록체인의 현 상태에
동의하도록 한다.  
따라서 모든 노드는 채굴 과정과 사용 중인 소프트웨어의 버전, 트랜잭션의 유효성 등에 정기적으로 합의를 달성해야 한다.  
<br>
비트코인 합의 알고리즘인 작업증명 방식(PoW, Proof of Work)은, 채굴 노드가 새로운 트랜잭션 블록을
검증할 수 있도록 한다.  
채굴의 결과인 논스로부터 나온 블록 해시는 채굴 노드가 충분한 작업을 완수했으며,  
해당 블록에 대한 유효한 해결책을 찾았음을 증명한다.  
<br>
작업 증명 기반 시스템에서의 채굴 과정은 막대한 양의 전력과 컴퓨터 자원을 수반하기 때문에,  
채굴에 대한 결과는 자신이 보유한 컴퓨터 파워에 기초한다.  
이렇게 해시값을 찾기 위한 컴퓨터들의 연산 파워를 해시 파워(Hash Power) 또는 해시 레이트(Hash Rate)라고 한다.  
<br>
채굴 노드들은 유효한 블록 해시를 찾아 새롭게 생성되는 비트코인을 보상으로 받기 위해 경쟁한다.  
비트코인 네트워크의 채굴 파워는 전 세계의 다양한 노드들에게 분산되어 있기 때문에,  
해시 파워는 어떤 단일 주체의 소유가 아니다.  
<br>
그런데, 만약 해시 파워가 충분히 분산화되어 있지 않으면 어떻게 될까?  
예를 들어, 단일 주체나 조직이 50%가 넘는 해시 파워를 가지게 된다면 어떻게 될까?  
<br>
이를 통해 벌어질 수 있는 문제를 51% 공격이라 부르며, 이는 다수 공격(Majority Attack)으로도 불린다.  

---

## Background
51% 공격은 단일 주체나 조직이 대다수의 해시 파워를 제어하여 네트워크를 중단시킬 수 있는 공격이다.  
51% 공격을 하기 위해서는 공격자가 트랜잭션 순서를 의도적으로 수정하거나 제외하기 위해 충분한 채굴 파워를 소유해야 한다.  
<br>
악의적인 주체가 충분한 채굴 파워를 소유하여 통제권을 쥐고 있게 되면, 자신이 발생시킨 트랜잭션을 되돌릴 수 있게 된다.  
이는 이중지불 문제로 이어질 수 있다.  
<br>
만약 악의적인 다수가 51% 공격을 성공하게 되면,  
공격자들은 트랜잭션의 일부나 전부가 승인되지 못하도록 하거나(트랜잭션 서비스 거부, Transaction Denial of Service),  
채굴자들이 채굴하지 못하도록 하고 채굴 작업을 독점(채굴 독점, Mining Monopoly)할 수 있다.  
<br>
그러나 악의적인 다수의 공격은 다른 이들의 트랜잭션을 되돌리거나 네트워크에 전송되는 트랜잭션을 거부할 수 없다.  
블록 보상을 변경하거나, 코인을 새롭게 생성하거나, 공격자의 소유가 아니었던 코인을 가로채는 작업 역시 발생하기 어렵다.  

---

## Mechanism
51% 공격은 네트워크 전체 해시 파워의 절반 이상을 확보하여 네트워크를 교란하게 시키는 공격법이다.  
그렇다면 어떻게 네트워크를 교란하게 시킬 수 있을까?  
<br>
이 공격을 위해서는 네트워크 전체 해시 파워의 50% 이상을 확보해야 한다.  
따라서 여기서 공격자는 블록체인 네트워크의 전체 해시 파워의 50% 이상을 확보했다고 가정한다.  
1. 공격자는 성능이 좋은 ASIC 장비 등을 도입하여 이더리움 클래식 네트워크에 접속한다.  
2. 공격자의 노드는 50% 이상의 높은 해시 파워로 채굴을 시작한다.  
그러나 블록체인 네트워크에 노드로 접속하게 해주는 클라이언트 프로그램을 수정해서,  
채굴한 블록들을 네트워크에 전파 (Broadcast)하지 않고 혼자 가지고 있는다.  
이런 식으로 혼자 블록들을 여러 개 생성한다.  
    2-1. 한편, 이더리움 클래식 네트워크에서는 정상적으로 블록을 생성하고 있을 것이다.  
    2-2. 그러나 악의적인 노드의 해시 파워는 네트워크의 전체 해시 파워보다 높기 때문에, 더 빠른 속도로 블록을 생성한다.  
    ![51-percent-attack](../../assets/img/51-percent-attack.png)
3. 이 상태에서, 공격자들은 정상 네트워크에서 트랜잭션을 발생시킨다.  
가령 10,000ETC를 `허술해 거래소`에 입금한다.  
이 입금 트랜잭션이 135번 블록에 기록되었다고 하자.  
`허술해 거래소`는 아무것도 모른 채로 평소대로 컨펌이 되면 입금을 처리해 준다.  
4. 공격자들은 30컨펌(7분 30초)을 기다렸다가 이더리움 클래식을 판다.  
    4-1. 이 시점에서 정상 네트워크에서는 165번 블록까지 생성되었을 것이다.  
    4-2. 반면, 네트워크의 해시 파워보다 더 해시 파워가 높은 공격자의 채굴 장비에서의 블록은,  
    180번까지 생성되었기 때문에, 공격자의 체인이 더 긴 상태이다.  
5. 공격자가 자신이 만든 체인을 정상 네트워크에 전파한다.  
    5-1. 네트워크에 있는 노드들은 두 개의 체인을 가지게 된다.  
    정상 네트워크에서 생성된 짧은 체인에 있는 블록들은 고아 블록이 되어 모두 취소된다.  
    > 블록체인에서는 이렇게 체인이 두 개로 나뉘었을 경우, 더 긴 체인을 선택하고, 나머지 체인을 취소한다.  
    > 이렇게 취소된 체인의 블록을 고아 블록(orphan blocks)이라고 하며, 이 과정을 **체인 재구성이**라고 한다.  
6. 이렇게 체인이 재구성되면,  
기존 체인에 있던 트랜잭션(10,000 ETC 입금 트랜잭션을 비롯한
정상적인 트랜잭션들)은 무효화된다.  
    6-1. 그러면 허술해 거래소 입금을 취소해야 하는데,  
    공격자들은 이미 코인을 다른 곳으로 송금한 뒤이기 때문에 취소할 수 없는 상황이 된다.  
    블록체인 입장에서는 10,000 ETC 송금이 없던 경우가 되기 때문에,  
    공격자들의 원래 계좌인 0x1234로 10,000 ETC 잔고가 생긴다.  
    6-2. 여기서 중요한 것은 공격자들이 만든 체인은 악의적인 체인이지만,  
    블록체인 입장에서는 가장 긴 체인이기 때문에 정상적인 체인이라는 점이다.  

공격자들이 정상 블록체인에서 다시 10,000 ETC를 자신들의 또 다른 계좌로 송금하면,  
공격자들의 입장에서는 10,000 ETC를 두 번 송금한 것이기 때문에 이중 지불이 된다.  
<br>
그러나 블록체인의 관점에서는 이전 송금은 아예 없던 일이 돼버리기 때문에,  
여전히 정상적인 트랜잭션들로 구성된다는 점에 주목해야 한다.  
<br>
왜냐하면 처음 10,000 ETC 전송 트랜잭션은 블록체인상에서 사라졌기 때문이다.  
결국 손해는 `허술해 거래소`가 입게 된다.  
<br>
일반 사용자 입장에서는 어떻게 대처해야 할까?  
<br>
입출금을 되도록 하지 않는 것이 최선이며, 특히 입금받을 때 주의해야 한다.  
자신이 받은 코인이 체인 재구성에 의해 블록체인상에서 취소될 수 있기 때문에,  
체인 재구성이 힘들 만큼 충분한 시간이 지난 후에 입금 처리를 해야 한다.  
거래소들이 입출금을 막거나 입금 컨펌 횟수를 늘리는 것은 이 때문이다.  
<br>
다른 작업 증명(Proof of Work) 방식을 사용하는 블록체인에도 이러한 위험이 이론상으로는 존재한다.  
그러나 비트코인에서는 전체 해시 파워가 매우 크기 때문에,  
51% 공격하기 위해서는 어마어마한 해시 파워가 필요하다.  
<br>
이를 전력 비용으로 환산하면 매우 많은 돈이 들기 때문에 일반적으로는 51% 공격으로부터는 안전하다고 믿고 있다.  
결론적으로, 작업 증명 방식을 사용하는 블록체인에서는 해시 파워가 곧 안정성을 의미한다.  
<br>
네트워크의 해시 파워가 낮으면 적은 전력으로도 51% 이상의 해시 파워를 얻을 수 있기 때문이다.  
> 마찬가지로, 지분 증명(Proof of Stake) 방식에서는 코인의 가치가 낮아지면 네트워크의 안정성이
떨어진다.  

51% 공격을 보면 알 수 있듯이, 블록 생성 시간은 큰 의미가 없다.  
비트코인은 10분에 한 번씩 블록을 생성하고, 이더리움은 15초에 한 번씩 블록을 생성한다.  
그렇다고 해서 이더리움이 비트코인에 비해 트랜잭션을 더 빠르게 처리하는 것은 아니다.  
<br>
왜냐하면 체인 재구성 공격에 대비해 일정 컨펌이 지난 후 입금을 처리해야 하므로,  
블록체인에 "얼마나 빠르게 기록되느냐"보다는 "얼마나 빠르게 컨펌되느냐"가 더 중요한 문제이기 때문이다.  
<br>
결국 이 확정 시간은 블록 생성 시간에 좌우된다기보다는 **해시 파워의 크기**에 영향을 받게 된다.  
해시 파워가 커서 체인이 안정될수록 확정 시간을 짧게 잡을 수 있다.  

---

## Probability
블록체인 네트워크가 안전한 이유는 블록체인 네트워크는 분산화된 노드 네트워크에 의해 유지되기 때문에,  
모든 참가자는 합의에 도달하는 과정에 협력하기 때문이다.  
<br>
작업 증명 블록체인의 경우,  
채굴 노드는 높은 해시 레이트를 가지고 있을수록 다음 블록의 유효한 논스값을 찾을 가능성이 커진다.  
채굴은 무수히 많은 해싱 시도를 포함하며, 컴퓨터가 더 큰 연산력을 가지고 있을수록,  
초당 더 많은 해싱 시도를 할 수 있다.  
<br>
몇몇 초기 채굴자들은 네트워크의 성장과 보안에 기여하기 위해 비트코인 네트워크에 합류했으나,  
통화로써의 비트코인의 가격이 치솟자, 수많은 신규 채굴자들이 블록 보상으로 코인을 받기 위해 네트워크에 합류하였다.  
<br>
비트코인이 안전한 이유 중 하나는 바로 이런 경쟁적 시나리오 때문이다.  
이러한 경쟁적 시나리오로 인해 비트코인의 규모는 매우 커졌으며,  
이에 따라 비트코인을 겨냥한 51% 공격은 일어나지 않을 것이다.  
<br>
블록체인의 규모가 충분히 커지면,  
한 개인이나 그룹이 다른 모든 참여 노드들을 압도할 수 있을 만큼의 컴퓨팅 파워를 보유할 가능성이 급격히 낮아지기 때문이다.  
<br>
이전에 승인된 블록은 모두 암호화 증명으로 연결되어 있기 때문에, 체인이 증가할수록 블록을 변경하는 것은 더욱 어려워진다.  
또한 블록이 더 많은 승인을 받을수록, 해당 블록을 변경하거나 되돌리는 데는 더 큰 비용이 들 수밖에 없다.  

---

## Solutions
**컨펌 횟수 증가**  
51% 공격은 블록체인 해시파워의 과반수를 확보하여 이중 지불 형태로 입금한 후 빼가는 것이다.  
반대로, 이중 지불 여부를 확인할 때까지 거래 확정을 늦춘다면 예방이 가능하다.  
<br>
그러나 거래 확정을 늦추기 위해 컨펌 횟수를 상향하면,  
안전성을 보장할 수는 있지만 거래 처리 속도가 느려져 사용성이 떨어진다는 단점이 있다.  
<br>
**지연 기능**  
51% 공격이 성공하려면 악의적인 노드가 거래 기록을 네트워크에 기록하기 전에, 따로 블록을 생성해야 한다.  
지연 기능은 블록체인 트랜잭션을 공증하는 공증 노드를 따로 둠으로써,  
전체 불변성을 보장하고 트랜잭션에 보안의 두 번째 계층을 제공한다.  

---

## Actual Cases
공격자가 비트코인 네트워크의 절반보다 더 많은 연산력을 가지는 것은 매우 어렵지만,  
규모가 작은 암호 화폐 네트워크에서는 가능하기도 하다.  
<br>
비트코인과 비교했을 때, 여러 알트코인들은 블록체인을 보호할 해시파워를 비교적 적게 가지고 있다.  
그리고 몇몇 알트코인들은 실제로 % 공격이 일어날 수 있을만큼 적게 가지고 있기도 하다.  
<br>
실제로 51% 공격이 발생한 암호 화폐들의 사례를 확인해 보자.  
<br>
**버지(Verge)**  
버지의 첫 번째 51% 공격은 2018년 4월 '포르노 허브'와의 제휴를 발표하기 약 주 전 발생했으며, 25만 버지 코인을 탈취당했다.  
두 번째 공격은 5월에 발생했으며, 3,500만 버지코인(시가 18억 원)이 넘는 피해가 있었다.  
<br>
51% 공격을 진행한 해커는 익명 게시판에 거래 시간을 기록하는 장치를 조작하여,  
쉽게 풀 수 있는 해시 함수로 된 블록을 한꺼번에 생산한 뒤, 코인을 채굴하는 식으로 공격했다고 설명했다.  
<br>
**모나코인(Monacoin)**  
모나코인은 2018년 5월, 블록보류 공격(Block Withholding Attack)이라고 불리는 공격을 당했다.  
이 공격으로 인해 모나코인 블록체인의 대규모의 체인 재구성이 일어났으며, 거래소는 약 1억 원 정도의 금전적 피해를 보았다.  
<br>
모나코인 블록체인은 2018년 5월 13일부터 15일까지 빈번하게 재구성되었으며, 최대 블록까지 재구성되기도 했다.  
이에 모나코인 유저들은 다른 거래소들에 모나코인 입금 시 컨펌 횟수를 늘리도록 연락하였으며,  
각 거래소는 입금을 정지하거나 컨펌 횟수를 늘리면서 해당 사건을 마무리했다.  
<br>
**비트코인 골드(Bitcoin Gold)**  
비트코인 골드 공격자는 네트워크 전체 해시파워의 51% 이상을 획득하여 블록체인을 제어했다.  
비트코인 골드와 같은 작은 네트워크에서도 절반 이상의 해시 파워를 얻는 것은 비용이 많이 들어가지만,  
이중 지불 공격을 병행하면 수익을 낼 수 있다.  
<br>
공격자의 주소 거래 내역에는 2018년 5월 16일 이후 해당 주소로 38만 8,200BTG(한화 201억 1900만 원)가 입금되었다.  
이후 비트코인 골드는 더 이상의 피해를 방지하기 위해 하드 포크를 결정하였다.  
<br>
**젠 캐시(ZEN Cash)**  
2018년 6월 2일 젠캐시에 대한 블록보류 공격으로 2만 3,152개의 젠 코인(한화 약 7억 원)에 대한 이중 지불 피해가 발생했다.  
젠 캐시 개발팀은 공격을 인지한 후 바로 해시 난이도를 높여 추가 공격을 막았다.  
<br>
**이더리움 클래식(Ethereum Classic)**  
2019년 1월 5일부터 약 사흘간 이더리움 클래식에서 총 11회의 이중 지불 공격이 발생했으며,  
이에 따라 8만 8,500 ETC(한화 약 12억 3천만 원)가 이중 지불되었다.  
<br>
코인베이스는 공격을 감지한 직후 이더리움 클래식을 주시하고 있다가,  
세 번째 공격이 발생한 이후 이더리움 클래식의 거래를 중지시켰다.  
공격 발생 후 이더리움 클래식은 컨펌 횟수를 400회까지 늘려 문제를 해결했다. 