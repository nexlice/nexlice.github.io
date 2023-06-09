---
title: Off-Chain
tags: 
 - Bitcoin Cash

---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다. 

# Off-Chain

---

## Lightning Network
![off-chain](../../assets/img/off-chain.png)  

라이트닝 네트워크는 양방향 채널이라는 아이디어를 기반으로,  
매우 저렴한 비용으로 거의 즉각적인 거래가 가능한 비트코인 ​​레이어(또는 레벨) 2의 솔루션이다.  
<br>
기본 블록체인과 마찬가지로 P2P 교환을 갖추고 있지만,  
자금 관리를 위임하지 않는 채널 네트워크에서도 돈을 교환할 수 있다.  
거래는 다른 모든 사람의 잔액에 대한 인증 역할을 하는 첫 번째와 마지막을 제외하고는, 오프체인이다.  

---

수많은 암호화폐가 트릴레마를 극복하기 위해 노력하고 있다.  
그중 하나인 라이트닝 네트워크(Lightning Network)는 기존 비트코인의 느린 처리 속도를 해결하고 빠른 속도를 구현하기 위해,  
개별 거래를 별도의 채널(Off-Chain)에서 처리한 후 그 결과만 블록체인에 기록하는 방식으로 작동하는 알고리즘이다.  
<br>
라이트닝 네트워크는 탈중앙화와 보안을 기본으로 두고 확장성을 높이기 위한 작업으로, 개별 노드 간에 일상적으로 반복되는 소액 거래 내역을 처리할 수 있도록 메인 블록체인 외부에 별도 채널을 구축한 오프체인 솔루션이다.  
<br>
여기서 거래된 내용은 모든 노드의 승인을 받지 않고 계약 당사자들끼리 합의를 통해 확정되고 블록체인에 저장되지도 않는다.  
반복적인 거래가 모두 끝난 후 오프체인을 닫을 때 비로소 최종 거래내역만 블록체인에 저장된다.  
승인 과정이 간단하고 반복적인 소액 거래가 블록체인에 저장되지 않으니 당연히 처리 속도는 빨라진다.  
<br>
그러나 오프체인 시스템 또한 탈중앙화 문제를 완벽하게 해결하지는 못한다.  
우선 블록체인 기술이 아니며 제3자 세력이 필요하므로 확장성 진영에서 이러한 시스템을 좋게 보지 않는다.  
<br>
확장성을 베이스로 두고 탈중앙화를 높이려는 진영은 본인들은 이미 트릴레마를 모두 극복했다고 말한다.  
서버 자체가 프라이빗 영역이라 봐도 무방하기 때문에 해커가 온라인에서 해킹하는 것이 사실상 불가능하기 때문이다.  
<br>
노드가 적으니 APT 공격을 하면 되지 않느냐는 반박이 나올 수 있지만,  
전 세계에 퍼진 노드를 APT로 공격한다는 발상 자체가 현재 기술로는 불가능하다.  
그러나 탈중앙화는 다른 문제로, 검증 노드가 소수이기 때문에 많은 사람에게 비난받고 있다.  
<br>
라이트닝 네트워크에는 이미 비트코인뿐만 아니라,  
비트코인의 DNA를 반을 보유하고 있는 퀀텀(Qtum) 역시 라이트닝 네트워크에 참여하고 있다.  
사실상 비트코인과 DNA가 같으면 라이트닝 네트워크를 사용하는 데 큰 지장이 없기 때문에,  
라이트닝 네트워크가 활발해지면, 비트코인의 확장성이 많이 개선될 것이다.  
<br>
이러한 방식으로 비트코인은 잠재적으로 확장성 요구 사항에 대한 솔루션을 찾았고  
수백만은 아니더라도 수천에 이르는 TPS에 도달할 가능성이 있다.  
<br>
Joseph Poon과 Thaddeus Dryja가 2016년 “The Bitcoin Lightning Network: Scalable Off-Chain Instatnt Payments”(비트코인 라이트닝 네트워크: 확장 가능한 오프체인 즉시 지급)이라는 논문과 함께 제안한 솔루션은 유명한 블록체인 트릴레마를 해결하기 위한 마지막 부분을 추가했다.  