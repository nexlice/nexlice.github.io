이더리움 논스
이더리움을 이용한 서비스를 구축하고 운영할 때 필수적으로 알아야 할 내용인, 트랜잭션을 구성하고 있는 필드 중 하나인 논스에 대해 알아보겠습니다.

이더리움 논스(Nonce)란 무엇인가?
모든 거래(Transaction)는 일회성입니다.
논스는 계정에서 보내는 트랜잭션에 할당된 번호입니다.
거래(Transaction)를 전송할 때 논스는 1씩 증가합니다.
논스는 계정에서 유일합니다. 동일한 논스는 존재하지 않습니다.
예) 최초 계정 생성 시 Nonce는 0입니다. (계정 기준으로 전송된 트랜잭션이 하나도 없을 때 )

전송한 Transaction1 : 1(Nonce) 전송한 Transaction2 : 2(Nonce) 전송한 Transaction3 : 3(Nonce).………전송한 Transaction10 : 10(Nonce)


논스 규칙
트랜잭션은 순서대로 이루어져야 합니다.
현재 계정의 Nonce가 1이라면, Nonce가 0인 트랜잭션을 전송할 수 없습니다.
이 경우 순서를 역행할 수 없으므로 오류가 발생합니다.
순번을 건너뛰지 않습니다.
논스는 순차적으로 증가하고 처리되기 때문에 논스가 3인 트랜잭션을 전송하려면, 논스의 값 0~2까지 전송한 내역이 있어야 합니다.
예를 들어, 논스가 3인 트랜잭션 전송 시, 현재 계정의 논스가 1일 경우, 트랜잭션이 처리되지 않고 Transaction Pool Queue에 남아있게 됩니다. 그리고 차후에 논스가 2인 트랜잭션을 전송하였을 경우 2, 3 이 연달아 처리됩니다.

논스가 필요한 이유
논스는 중복되지 않고 순서가 있기 때문에, 같은 논스를 가진 여러 트랜잭션 전송이 발생할 경우엔 해당 논스 중 제일 높은 가스비를 지불한 트랜잭션이 처리됩니다. 이더리움에서는 이러한 방법으로 이중 지불 문제를 방지합니다.

그럼, 논스를 통해 트랜잭션을 취소할 수 있을까요?
결론적으로 트랜잭션이 네트워크에 정상적으로 전파되었다면 취소하는 방법은 존재하지 않습니다. 그러나 논스를 기존보다 높게 설정되었거나, 너무 낮은 가스를 지불하였을 경우 아직 Transaction Pool에 남아있는 상태(Pending)라면 논스를 이용하여 해당 트랜잭션을 재전송하여 취소된 효과를 보실 수 있습니다.

참고 : [check-status-of-ethereum-transaction](https://help.myetherwallet.com/en/)

