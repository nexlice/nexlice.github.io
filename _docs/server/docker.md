---
title: Docker
tags: 
 - container
 - vm
 - image
 - registry

description: Learn about the concept of Docker!
---

>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

<!-- {% include alert.html type="danger" title="Warning!" content="이 문서는 아직 미완성 문서입니다." %} -->

# Docker
![docker]()  
도커는 리눅스 컨테이터 기술을 기반으로 하는 오픈 소스 서비스이다.  
도커를 통해 어플리케이션 실행 환경을 코드로 작성할 수 있으며, OS를 격리화하여 관리한다.  
도커의 등장 배경과 중요한 개념들에 대해 알아보자.  

## Backgrounds
컨테이너가 있기 전에는 실제로 화물 수송에서 물자를 그물망에 실어 옮기곤 했다.  
하지만 컨테이너가 생긴 이후로, 물류에는 혁신이 일어났다.  

- 물자를 싣고 내릴 때, 선박이 입항해 있는 시간을 획기적으로 단축해 준다.  
- 물자를 싣고 내릴 때 필요한 인력(분류하는 사람, 짐옮기는 사람, 감독하는 사람)을 대폭 감소 시킨다.  

개발자들은 이처럼 물자의 수송에 획기적인 단축을 가져다준 컨테이너 기술을,  
"**소프트웨어 수송, 즉 배포**에 사용할 수는 없을까?" 라는 생각을 하기 시작했다.  
그 결과로 `리눅스 컨테이너(lxc)`를 만들기에 이른다.  
<br>
리눅스 컨테이너 기술은 그 자체로 훌륭하고 완성된 기술이었지만,  
애플리케이션을 쉽게 컨테이너화할 수 있는 생태계 혹은 커뮤니티가 없었다.  
2013년에 등장한 `Docker`는 `Docker Hub`라는 소프트웨어 저장소와 함께 빠르게 성장했고,  
그 결과 개발자들은 쉽게 애플리케이션을 포장하고, 컨테이너 방식으로 실행할 수 있게 되었다.  
![docker-image]()  
"컨테이너 방식으로 애플리케이션을 실행한다"라는 개념이 아직은 잘 와닿지 않을 수 있다.  
컨테이너 기술의 장점은, `실행 환경에 구애받지 않고, 애플리케이션을 실행할 수 있다`는 것이다.  
이는 다시 말해, 어플리케이션 실행이 어떠한 **환경**에 구애를 받는다는 말이다.  

### Linux Container
리눅스 컨테이너는 리눅스 기반의 기술 중 하나로,  
필요한 라이브러리와 어플리케이션을 모아서 마치 별도의 서버처럼 구성한 것을 말한다.  
컨테이너를 이루는 네트워크 설정, 환경 변수 등의 시스템 자원은 각 컨테이너가 독립적으로 소유하고 있다.  

## Why Docker
도커는 컨테이너를 사용하기 때문에 유용하다.  
컨테이너 방식의 장점은 다음과 같다.  

- 환경 표준화
    - 의존성 충돌 문제를 해결해 준다.  
    - 개발과 배포 환경을 일치시킨다.  
- 리소스 격리성을 보장한다.  
- 수평 확장을 쉽게 해 준다.  
- 각 서버에 새로운 내용을 배포하기 쉽게 만들어준다.  

각 장점이 어떻게 나타나는지 하나씩 확인해보자.  

### Dependency Collision Problems
- 환경 의존성
어떤 어플리케이션은, 해당 어플리케이션을 실행하기 위해 반드시 어떤 환경이 구축되어 있어야 한다.  
이를테면, 윈도우용 프로그램을 실행하려면 윈도우 운영체제가 필요하다.  
![.netframework-dependency-error]()  
이처럼 어떤 프로그램 (A) 실행에 다른 프로그램 (B)가 반드시 필요한 경우,  
**"프로그램 A는 프로그램 B에 의존 관계를 가지고 있다" 라고 말한다.**  

- 버전 의존성 충돌
어떤 두 어플리케이션이 php 프로그램에 대해 의존 관계를 가지면서,  
서로 다른 php 버전을 요구하는 경우를 생각해보자.  
<br>
일반적으로 한 컴퓨터에 여러 버전의 동일한 어플리케이션이 설치되지 않으므로,  
php의 의존 관계를 가지고 있는 다른 두 애플리케이션 중의 하나는 제대로 된 실행을 보장할 수 없다.  
<br>
이와 같은 상황을 **의존성 충돌**이라고 한다.  

### Container
컨테이너는 어플리케이션의 의존성, 네트워크 환경, 파일 시스템에 구애받지 않고,  
도커라는 기술 위에 실행될 수 있도록 만든 어플리케이션 상자이다.  
<br>
컨테이너 기술은 애플리케이션을 컨테이너 내에 구성하여 위의 문제들을 해결한다.  
즉, 컨테이너에서 실행 중인 어플리케이션은 어떠한 의존성도 공유하지 않고, 각자 고유의 의존성을 포함하고 있다.  
이는 각 컨테이너가 실행 환경이 격리되어 있기 때문에 가능하다.  

#### Docker Container Lifecycle
![docker-container-life-cycle]()  

### Isolation
하나의 컴퓨터 내에 서로 다른 버전의 어플리케이션 (위의 예시로는 php)가 설치될 수 있는 이유는,  
컨테이너 하나하나가 어플리케이션 실행과 관련해서 높은 수준의 격리를 제공하기 때문이다.  
<br>
컨테이너는 다음을 격리하고, 독립적으로 소유(`구획화`)한다.  

1. 프로세스
    - 특정 컨테이너에서 작동하는 프로세스는 기본적으로 그 컨테이너 안에서만 액세스할 수 있다.  
    - 컨테이너 안에서 실행되는 프로세스는 다른 컨테이너의 프로세스에 영향을 줄 수 없다.  
2. 네트워크
    - 컨테이너 하나에 하나의 IP 주소가 할당되어 있다.  
3. 파일 시스템
    - 컨테이너 안에서 사용되는 파일 시스템은 구획화 되어 있다.  
    그래서 해당 컨테이너에서의 명령이나 파일 드으이 액세스를 제한할 수 있다.  

#### IP
IP 주소가 컨테이너마다 할당 되는 것이 어떤 이점이 있을지 알아본다.  
서버 관리자에게 다음과 같은 요구사항이 입력된다고 가정해보자. 
- 웹 서버 1 : IP는 A로, 포트 번호는 A-1으로, 방화벽 규칙은 a의 규칙을 이용한다.  
- 웹 서버 2 : IP는 B로, 포트 번호는 B-1으로, 방화벽 규칙은 b의 규칙을 이용한다.  

IP 주소는 인터넷 상에 있는 컴퓨터의 고유한 주소이다.  
IP 주소 덕분에 인터넷 상의 한 컴퓨터에서 다른 컴퓨터로 데이터를 주고 받을 수 있다.  
<br>
하지만 위 상황은 서버가 하나밖에 없어서, IP 주소를 구분하기 위해 브리지 설정을 변경해야하고,  
방화벽 규칙 a와 b가 서로 충돌이 나고 있는 상황이다.  
<br>
실제로는 하나의 컴퓨터를 사용하지만, 여러 개의 컴퓨터를 이용하는 것처럼 하기 위해 `리소스 격리성`을 활용한다.  
리소스 격리성을 제공하는 기술로는 도커와, 가상 머신이 있다.  

### Container vs VM
`Virtual Machine`이란, 하나의 호스트(주인) 컴퓨터 위에 여러 개의 독립적인 컴퓨터가 작동할 수 있게하는 기술이다.  
대표적으로 `VMware`, `VirtualBox`, `Parallels`가 있다.  
<br>
도커를 비롯한 리눅스 컨테이너 기술은 가상 머신의 접근 방법과 다르다.  
하지만 컨테이너 역시 가상 머신과 비슷한 수준의 격리성을 제공한다.  
<br>
![left-docker-right-vm]()  
위의 그림에서 왼쪽은 도커, 오른쪽은 가상 머신을 설명한다.  
가상 머신과 도커는 격리성을 제공하기 때문에, 어플리케이션마다 다른 컴퓨터에서 실행되는 것처럼,  
IP나 Port를 다르게 설정할 수 있다.  
<br>
둘의 차이점은 다음과 같다.  
- 도커는 가상머신만큼 견고한 격리성을 제공하지는 않는다.  
- 도커는 리눅스 컨테이너를 이용한 기술로, OS위에 다른 OS를 실행하는 것이 아니므로,  
가상머신보다 더 좋은 성능을 낼 수 있다.  
- 어플리케이션에 대한 환경 격리성을 중심으로 한 VM과는 달리,  
도커는 Container의 관점에서 개발자와 사용자 커뮤니티를 중심으로 혜택을 제공한다.

### Development Environments
여러 개발자가 하나의 어플리케이션을 만들기 위해, 보통 비슷한 개발 환경을 구축한다.  
하지만 보통의 경우, 그 과정이 빠르게 진행되지 않는다.  
<br>
리눅스만 하더라도, 배포판에 따라 전혀 다른 어플리케이션 설치 과정이 진행된다.  
이러한 과정 주엥 발생하는 사소한 실수나 사전 설치 항목의 부재는 문제 해결에 많은 시간을 소모하게 한다.  
<br>
도커는 이러한 문제를 해결해준다.  
도커는 단일 소프트웨어 패키지를 설치도 용이하게해줄 뿐더러,  
`Docker Compose`툴을 이용해 `YAML` 파일과 명령어 하나로 모든 어플리케이션 실행 환경을 구성해준다.  
```bash
docker-compse up
```
즉, 도커는 다음 문제를 해결해준다.  
- OS에 상관 없이 즉시 어플리케이션 실행 환경을 만들 수 있다.  
- 개발을 컨테이너 위에서 진행할 경우, 모든 개발팀이 동일한 환경하에 개발을 진행할 수 있다.  

###  Deployment Environments
앞서 설명한 실행 및 개발 환경의 일치 이슈는 서비스 배포에 환경에서도 동일하게 적용된다.  
웹 서비스의 배포란, "어떤 어플리케이션이 특정 런타임 환경 위에서 실행되고, 사용자에게 이를 제공한다"를 뜻한다.  
이는 그저 서비스를 인터넷 상에 공개적으로 노출하느냐, 내 컴퓨터 위에서 private하게 작동하느냐의 차이일 뿐이다.  
<br>
그래서 이제는 배포의 패러다임에 달라졌다.  
서버는 컨테이너에 담긴 어플래케이션을 실행하는 방식으로 서비스를 제공한다.  
<br>
따라서 AWS의 EC2 상에 도커를 설치하거나,  
도커 컨테이너를 EC2 서버에서 실행할 수 있게 하는 서비스인 ECS를 이용하여 쉽게 어플리케이션을 배포할 수 있다.  
<br>
~~제 컴퓨터에서는 작동 되는데요?~~라는 말은 컨테이너 환경에서는 더 이상 유효하지 않다.  
![it-works-on-my-machine]()  

### Horizontal Scaling and Distribution of New Content
우리가 매일 사용하는 글로벌 웹 서비스는 전 세계인들이 사용하므로 그 트래픽이 엄청나다.  
검색 서버는 단 하나의 컴퓨터가 아니다.  
<br>
서비스 제공자들은 이러한 트래픽 분산을 위해 `프록시 서버`응 운영하며,  
프록시 서버는 여러 대의 동일한 검색 서버 중 한 군데를 이용할 수 있도록 돕는다.  
이러한 서버를 리버스 프록시의 한 종류인 `로드 밸런서`라고 부른다.  
![load-balancer]()  
컨테이너 기술의 가장 큰 장점은 **실행 환경의 일치**이다.  
더 많은 트래픽으로 인한 서버 증설에 컨테이너 기술은, 아주 활발하게 이용된다.  
<br>
동일한 어플리케이션 구성(이미지)를 바탕으로, 새로운 서버에 해당 어플레케이션을 컨테이너로 실행하고,  
로드 밸런서에 이 서버를 추가하기만 하면 된다.  
> AWS는 서버를 만들고 삭제하는 일을 자동으로 해주기도 한다.  

이러한 기술을 응용하여, 새로운 버전의 어플리케이션을 여러 서버 중 몇 대에만 운영하여 테스트하는 방법도 가능하다.  
이를 통해 새 버전의 어플리케이션에 발생할 수 있는 문제들을 미리 확인하고,  
이러한 문제가 사용자 전체에게 영향을 끼치지 않도록 만들 수 있다.  
![orchestrator-test]()  
쿠버네티스와 같이 "오케스트레이션 도구"라고 부르는 것들이 이러한 일을 해주는 도구이다.  
이는 결국 컨테이너 기술 덕분에 가능한 것이다.  

## Image
실행되는 모든 컨테이너는 이미지로부터 생성된다.  
이미지는 어플리케이션 및 어플리케이션 구성을 함께 담아놓은 템플릿으로, 이를 이용해 즉시 컨테이너를 만들 수 있다.  
<br>
이미지를 이용해 여러 개의 컨테이너를 생성할 수 있다.  
이는 어플리케이션의 수평 확장을 가능하게 한다.  
<br>
이미지는 기본 이미지(base image)로부터 마치 git을 사용하는 것처럼, 변경 사항을 추가/커밋 해서 또 다른 이미지를 만들 수도 있다.  
이를테면, node.js로 작성된 어플리케이션을 이미지로 만들고 싶은 경우,  
node.js 이미지를 기본 이미지로 삼고, 내가 만든 어플리케이션을 추가한 다음 이미지화 할 수 있다.  

## Registry
이미지는 레지스트리에 저장된다.  
대표적인 이미지 레지스트리로는 Docker Hub, Amazon ECR이 있다.  
도커 CLI에서 이미지를 이용해 컨테이너를 생성할 때, 호스트 컴퓨터에 이미지가 존재하지 않으면,  
기본 레지스트리부터 다운로드한다.  