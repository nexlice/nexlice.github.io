---
title: IPFS
tags: 
 - protocol
 - DAG
 - DHT
 - Decentralization
 - Content-addressing
 - Participation

---

> 본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

# IPFS
IPFS(InterPlanetary File System)는 Git, BitTorrent, Kademlia, Bitcoin 등과 같은 서비스에서 영감을 받아 시작한  
무료 오픈 소스 프로젝트이다.  
<br>
“인터넷과 웹의 인프라를 발전시키자"라는 비전으로 현재 약 수천 명의 컨트리뷰터와 함께 운영되고 있다.  
<br>
IPFS를 간단히 정의하자면 아래와 같다.  
- **분산형 파일 시스템**에 데이터를 저장하고 인터넷으로 공유하기 위한 프로토콜  
- **P2P(peer-to-peer)** 네트워크  

> 기존의 HTTP 프로토콜 방식은 데이터가 위치한 곳의 주소를 찾아가서 요청한 콘텐츠를 한 번에 가져오는 방식이었지만,  
> IPFS는 전 세계 여러 컴퓨터에 분산 저장된 각 데이터 조각으로 잘게 나눠서 가져온 후,  
> 하나로 합쳐서 보여주는 방식으로 동작한다.  

IPFS는 현재도 진행 중인 프로젝트로써, 관련한 문서와 포럼은 실시간으로 발전하고 있다.  
- Github: https://github.com/ipfs/ipfs  
- 문서: https://docs.ipfs.io/  
- 포럼: https://discuss.ipfs.io/  

현재 Go, 자바, 자바스크립트, 파이썬 등에서는 IPFS 클라이언트 라이브러리를 활용 가능하다.  

---

IPFS는 프로토콜이자 파일 시스템, 웹, 모듈러, 암호화, p2p, CDN, 네임서비스 모든 것을 아우른다.  

**프로토콜**  
- content-addressed 파일 시스템
- 콘텐츠 전달
- Kademlia + BitTorrent + Git 결합

**파일 시스템**  
- 디렉토리, 파일 기반
- 마운트 가능한 파일 시스템(FUSE를 통해)  

**웹**  
- 전통적인 웹과 같이 문서를 보는 데 사용 가능  
- HTTP를 통해 파일에 액세스 가능  
- 브라우저 및 확장 프로그램은 ipfs:// 또는 dweb:/ipfs/ 의 URL, URI 스키마를 직접 사용하는 방법을 학습 가능  
- Hash-addressed 콘텐츠가 신뢰성을 보장  

**모듈러**  
- 모든 네트워크 프로토콜의 연결 계층  
- 라우팅 레이어  
- DHT(Kademlia/Coral) 라우팅 레이어 사용  
- 경로 기반 네이밍 서비스 사용  
- BitTorrent에서 차용한 블록 교환 사용  

**암호화**  
- 각 콘텐츠에 암호화 해시 주소 지정  
- 블록 수준 중복 제거  
- 파일 무결성 및 버전 관리  
- 파일 시스템 수준에서 암호화 및 서명 지원  

**p2p**  
- 전 세계 peer-to-peer 파일 전송  
- 완전한 분산 아키텍처  
- 중앙 실패 지점 없음  

**CDN**  
- 로컬에서 파일을 추가하면 전 세계에서 사용 가능  
- 캐싱 친화적  
- BitTorrent 기반의 네트워크 대역폭 분포  

**네임 서비스**  
- SFS에서 영감 받은 네임 서비스, IPNS  
- PKI(공개키 암호화) 기반 글로벌 네임스페이스  
- 신뢰 사슬 구축  
- 다른 NS 서버와 호환  
- DNS, .onion, .bit 등을 IPNS에 매핑 가능  

![ipfs](../../assets/img/ipfs.png)  
IPFS를 사용하게 되면 해당 컴퓨터는 필요한 파일들을 다운로드하는 것과 동시에 파일들을 나누어 주는 역할을 한다.  

---

## Features
IPFS 대표적인 특징은 아래와 같다.  
- 분산화(Decentralization)  
- 콘텐츠 어드레싱(Content-addressing)  
- 참여(Participation)  

### Decentralization
IPFS는 중앙 서버가 아닌 분산된 환경의 여러 피어로부터 파일을 다운로드할 수 있다.  
- **안정적인 인터넷 지원**  
중앙 서버에 오류가 생기면 파일 다운로드가 불가능한 기존의 구조 대비, 다른 곳에서 동일한 웹 페이지를 얻을 수 있다.  
- **콘텐츠를 검열에 대한 내성**  
파일이 분산된 환경에서 전달된다는 특성으로 인해 특정 정보에 접근하는 것을 막거나 검열하는 것을 어렵게 한다.  
- **높은 웹 속도**  
요청하는 컴퓨터가 멀리 떨어져 있거나 인터넷이 연결되지 않은 상황에서도,  
주변의 가까운 피어에서 빠르게 파일을 받아올 수 있다.  

---

### Content Addressing
`/ipfs/QmXoypizjW3WknFiJnKLwHCnL72vedxjQkDDP1mXWo6uco/wiki/Codestates.html`  
<br>
콘텐츠 어드레싱이란 콘텐츠를 주소 기반으로 표현한다는 것이다.  
IPFS 콘텐츠의 URL은 위와 같은 형태이다.  
<br>
`/ipfs/` 다음의 문자열을 콘텐츠 식별자(content identifier, CID)라고 하며,  
이를 통해 여러 피어로부터 콘텐츠를 가져올 수 있다.  

- https://en.wikipedia.org/wiki/Codestates  
- /Users/Codestates/Document/codestates_content.doc  

위와 같은 전통적인 URL 또는 파일 경로는 해당 위치를 기반으로 파일을 식별한다.  
<br>
이와 달리 IPFS는 파일에 포함된 내용을 기준으로 파일의 주소를 식별한다.  
쉽게 말해, 콘텐츠의 내용을 통해 콘텐츠에 접근할 수 있다.  
<br>
IPFS에서는 내용을 기준으로 파일의 주소를 식별하는 콘텐츠 식별자를 만들 때 해시를 사용한다.  

#### Hash Value
왜 콘텐츠 식별자로 해시값을 쓰는 걸까?  
모든 콘텐츠는 고유하다는 특징이 있다.  
따라서 해시를 사용하면 고유한 콘텐츠를 쉽게 표현할 수 있다.  
<br>
해시는 원본 콘텐츠가 1bit라도 변경되면 완전히 새로운 값을 가지게 된다는 특성(쇄도 효과)이 있는데,  
그렇기에 IPFS의 URL은 변경될 수 없다.  
- 웹 페이지의 텍스트가 변경되면 새 버전은 새롭고 다른 주소를 갖는다.
- 콘텐츠를 다른 주소로 이동할 수 없다.  

> 하지만 매번 콘텐츠가 업데이트되거나 변경될 때마다 새로운 링크를 보내는 것은 비효율적이라고 생각할 수 있다.  
> 그러한 부분은 [IPNS](https://docs.ipfs.tech/concepts/ipns/) , [MFS(Mutable File System)](https://docs.ipfs.tech/concepts/file-systems/#mutable-file-system-mfs) 및 [DNSLink](https://docs.ipfs.tech/concepts/dnslink/)를 참고해서 보완이 가능하다.  

IPFS를 사용하는 것은 참여적이고 협력적이라는 점을 기억하는 것이 중요하다.  
아무도 콘텐츠 식별자를 가지고 있지 않은 경우 해당 콘텐츠를 얻을 수 없다.  
반대로 해당 콘텐츠 식별자를 단 한 사람이라도 가지고 있다면 해당 콘텐츠를 지울 수 없다.  

---

### Participation
IPFS의 기본적인 아이디어는 사람과 컴퓨터가 통신하는 방식을 바꾸는 것이다.  
오늘날의 웹(WWW)은 **소유권과 액세스**를 기반으로 구성되어 있어,  
파일을 소유한 사람이 액세스 권한을 부여하기로 한 경우에만 파일을 받을 수 있다.  
<br>
반면 IPFS는 **소유와 참여**를 기반으로 동작하며,  
많은 사람이 서로의 파일을 소유하고 사용할 수 있게 만드는 데 초점을 맞추었다.  
즉, IPFS는 사람들이 적극적으로 참여한다는 가정하에만 정상적으로 작동한다. 

---

## Operations
IPFS는 peer-to-peer 네트워크로, 전 세계에 분포되어 있는 피어를 통해 접근할 수 있다.  
IPFS의 동작 방식을 이해하기 위해서는 3가지의 원칙을 알아야 한다.  
- 콘텐츠 어드레싱(Content-addressing)을 통한 고유 식별  
- 방향성 비순환 그래프(DAG)를 통한 콘텐츠 연결  
- 분산 해시 테이블(DHT)을 통한 콘텐츠 검색  

---

### Content Addressing
위에서 언급한 것처럼, IPFS는 파일의 내용을 해시화하여 콘텐츠 식별자(CID)를 생성한다.  
해시는 원본 콘텐츠에 비해 짧아 보일 수 있지만 기원한 콘텐츠에 대해 고유한 값이다.  
<br>
다른 많은 분산 시스템도 해시를 통해 콘텐츠 식별뿐 아니라,  
함께 콘텐츠를 서로 연결하는 수단으로 사용한다. (Git 커밋, 블록체인 등)  
<br>
하지만 이러한 시스템의 기본 데이터 구조는 상호 운용 가능하지 않고 서로 연동되지 못하기도 한다.  
이러한 문제를 해결하기 위해 [IPLD](https://ipld.io/)이라는 프로젝트가 시작되었다.  
IPLD는 해시 연결 데이터 구조 사이를 변환하여 분산 시스템 전반에 걸쳐 데이터를 통합할 수 있도록 한다.  

---

### DAG
IPFS 및 다른 많은 분산 시스템은 DAG(방향성 비순환 그래프) 자료 구조를 사용한다.  
특히 각 노드에는 노드 콘텐츠의 해시가 있는 Merkle DAG를 사용힌다.  
이는 콘텐츠 어드레싱 개념과 일맥상통하는 부분이 있다.  
<br>
IPFS는 디렉토리와 파일을 나타내는 것에 최적화된 Merkle DAG를 사용하는데,  
이때 다양한 방법으로 Merkle DAG를 구성할 수 있다.  
> Git은 그 안에 여러 가지 버전을 가진 Merkle DAG를 사용한다.  

콘텐츠를 하나의 Merkle DAG로 만들기 위해서는 먼저 콘텐츠를 블록 단위로 분할해야 한다.  
콘텐츠를 블록들로 나누어서 두 개의 유사한 파일이 있는 경우 Merkle DAG의 일부를 공유할 수 있다.  
<br>
즉, 다른 Merkle DAG의 일부가 동일한 데이터 하위 집합을 참조할 수 있다.  
이렇게 하면 BitTorrent처럼 매번 완전히 새로운 파일을 만드는 대신 새롭거나 변경된 부분만 전송받을 수 있다.  
![ipfs-active-active](../../assets/img/ipfs-active-active.png)
출처: https://explore.ipld.io/#/explore/QmSnuWmxptJZdLJpKRarxBMS2Ju2oANVrgbr2xWbie9b2D  
<br>
Merkle DAG에서 모든 것은 CID가 있다.  
폴더 그 자체, 폴더에 있는 파일들, 해당 파일은 블록까지 모두 CID를 가진다.  
요약하자면 IPFS는 콘텐츠에 CID를 부여하고 Merkle DAG를 통해 해당 콘텐츠를 함께 연결할 수 있다.  

---

### DHT
어떤 피어가 콘텐츠를 호스팅하고 있는지 탐색하기 위해 IPFS는 분산 해시 테이블(DHT)을 사용한다.  
해시테이블은 키와 값으로 구성된 데이터베이스이며,  
분산 네트워크에 참여하는 모든 피어에게 나누어져 존재하는 하나의 테이블이다.  
그래서 콘텐츠를 탐색하기 위해서는 이러한 피어들에게 질의를 해야한다.  
<br>
IPFS는 DHT를 제공하고 서로 연결하고 소통하는 피어를 처리하기 위해 [libp2p](https://libp2p.io/)라는 프로젝트를 제공한다.  
> IPLD와 같이 다른 분산 시스템에서도 사용될 수 있다.  

콘텐츠가 어디에 있는지, 즉 어떤 피어가 콘텐츠를 구성하는 각 블록을 저장하는지만 알게 되면,  
DHT를 사용하여 해당 피어의 현재 위치를 알아낼 수 있다.
<br>
콘텐츠를 찾고 해당 콘텐츠의 현재 위치를 알아냈다면, 이제 해당 콘텐츠의 내용을 가져와야 한다.  
따라서 내용을 보기 위해서는 한 번 더, 총 두 번의 쿼리가 필요하다.  
> 순서 : 피어의 현재 위치 찾기 → 콘텐츠 내용 찾기

다른 피어에게 블록을 요청하고 블록을 보내기 위해서는 [Bitswap](https://github.com/ipfs/specs/blob/main/BITSWAP.md)이라는 모듈을 사용한다.  
Bitswap을 사용하면 원하는 콘텐츠를 가지고 있는 피어에 연결하고,  
원하는 목록(관심 있는 모든 블록 목록)을 보내고 요청한 블록을 받을 수 있다.  
<br>
요청한 블록이 도착하면 콘텐츠를 해시하여 CID를 얻고 이를 요청한 CID와 비교함으로써 정확한 데이터를 받았는지 검증할 수 있다.  
> Bitswap과 더불어서 [Graphsync](https://github.com/ipld/specs/blob/master/block-layer/graphsync/graphsync.md)와 같은 다른 복제 프로토콜도 논의하고 있다.  

## References
- https://docs.ipfs.io/  
- https://github.com/ipfs/ipfs  
- https://www.youtube.com/watch?v=Z5zNPwMDYGg  
