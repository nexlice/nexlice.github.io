---
title: Package Manager
tags: 
 - package manager
 - apt
 - brew
 - wget
 - pip
 - pip3

description: Learn about package manager!
---

# Package Manager
>   본 글은 Codestates BEB 코스의 자료에서 내용을 가져와 작성하였음을 알립니다.  

## The advent of package manager
패키지 매니저는 왜 태어났을까?  
프로그램을 독립적으로 설치하는 데에는 한가지 큰 단점이 있다.  
여러 프로그램을 개별로 설치하기 위해서는, 각각의 프로그램이 저장된 위치를 모두 알아야한다.  
모든 프로그램이 한 곳에 저장되어 있으면 좋겠지만, ~~당연히도~~ 여러 군데에 퍼져있다.  
이러한 상황에서 우리는 다음과 같이 행동해야 한다.  

- 즉, 해당 프로그램을 저장하고 있는 저장소의 위치를 모두 알아야한다.
- 업데이트 여부르르 확인하게 위해서도 주기적으로 저장소를 방문해야한다.

이런 단점을 보완하기 위해서 생긴 도구가 바로, **패키지 매니저**이다.  

---
## What does a package manager do?
패키지 매니저는 패키지의 설치, 변경, 삭제 등 관리를 편리하게 해주는 도구이다.  
스마트폰으로 비유하자면 앱스토어와 그 역할이 비슷하다.  
패키지 매니저는 모든 패키지의 저장소 위치를 저장하고 있다.  
사용자가 pm에게 특정 프로그램의 설치를 요청하면,  
패키지 매니저는 패키지가 저장된 위치에서 패키지를 다운로드 받아 설치 프로그램을 실행한다.  

---

## Homebrew
Homebrew는 맥의 패키지 매니저이다.  
먼저 Homebrew를 사용하기 위해서는 [brew.sh](https://brew.sh)에 방문하여 시키는 대로 해보자.  

---

#### 잘 쓰던게 안되던데?
어떤 명령어가 안되는 이유에는 여러가지가 있다.  
그중 필자가 겪은 에러로는 `invalid active developer path`이다.  
이는 맥 os를 업데이트 해줬을 때 일어나는데,  
os를 업데이트하고 나서 다음 명령어를 통해 `Xcode command line tool`을 재설치하면 해결된다.
```bash
xcode-select --install
```

`brew doctor` 명령어를 통해서 문제점을 진단할 수도 있다.  
brew를 통해 설치한 프로그램들이 정상인지 확인한다.  
Homebrew 공식 문서에서는 `update`를 두번 실행한 후, `doctor`를 사용하기를 권장한다.

또한 brew는 default로 낡은 버전의 formula를 삭제하지 않는다.  
따라서 이전 버전이 시간이 지나면서 쌓이게 된다.  
물론 버전을 여러개 옮기면서 쓴다면 문제가 되겠지만, 공간을 확보하고 싶다면 `cleanup` 을 사용해보자.  
```bash
# Run brew update twice and brew doctor (and fix all the warnings) before creating an issue!
brew doctor

# frees up space in macOS and Linux devices by removing old versions of formulae 
# and small kegs of data (about 20-80 MB each). 
brew cleanup

```

---
### Formulae and Casks
`brew list`를 실행해보면 Formulae가 있고 Casks가 있다.  
둘의 차이점에 대해서 알아보자.  

---

`Homebrew-Cask`는 Homebrew의 extension으로 구글 크롬이나 Atom과 같은 GUI 어플리케이션을 설치할 때 사용한다.  
본래 독립적으로 시작되었으나, Cask maintainer들이 Homebrew의 코어 팀과 같이 일한다고 한다.  

Homebrew는 자신의 package definition file들을 `Formulae`라 한다.  
*fomulae는 formula의 영국식 복수이다.*  
`Homebrew-Cask`는 자신의 package definition file들을 `Casks`라 한다.  

---

`Cellar`(지하 창고)는 Homebrew가 설치한 것들을 저장하는 곳이다.  
이곳의 default path는 `/usr/local/Cellar`이다.  
Apple Silicon의 경우, `/opt/homebrew/Cellar`이다.  
Homebrew는 이후 `symlink`를 standard location으로부터 추가한다.  
*`symlink`란, 링크를 연결하여 원본 파일을 직접 사용하는 것과 같은 효과를 내는 링크를 말한다.*
*윈도우의 바로가기 같은 것!*
*특정 폴더에 링크를 걸어 NAS, library 원본 파일을 사용하기 위해서 심볼릭 링크를 사용한다.*

---

`tap`은 formulae의 source이다.  
기본값은 `homebrew/core`이지만, 사용자가 더 추가할 수 있다.  
개인 소프트웨어를 위한 formula를 만드는 가장 쉬운 방법은 `homebrew-<something>` 이름을 가진 GitHub 레포를 만드는 것이다.  
이곳에 formula 파일을 넣고, `brew tap <username>/<something>` 을 실행하여,  
Homebrew installation에 새로운 formulae의 source를 추가하고, 해당 source의 모든 formulae에 접근할 수 있다.  

#### Examples
`brew install git` 명령어를 실행한다고 하자.  
이떄 brew는 다음 두 행동을 실행한다.  
1. Homebrew는 `git`바이너리를 `/opt/homebrew/Cellar/git/``<version>/bin/git` 에 설치한다.  
2. Homebrew는 `/opt/homebrew/bin/git`으로부터 그 바이너리 파일로 symlink를 추가한다.  

이 행동은 Homebrew가 `brew`명령어로 어떤 패키지를 설치했는지, 그리고 다른 수단으로 설치했는지 추적할 수 있도록 한다.  

[내용 출처 :  Stack Overflow](https://stackoverflow.com/questions/46403937/what-is-the-difference-between-brew-install-x-and-brew-cask-install-x)  

---

## apt
apt는 Advanced Package Tool의 이니셜로, 우분투의 패키지 매니저이다.  

---
## wget  
wget은 url을 통해서 파일을 다운로드 받게 해주는 프로그램이다.  

---
## brew vs pip
`pip`은 파이썬을 위한 packager이다.  
`pip`을 통해서는 `python-things`만 설치 가능해야한다.  
`homebrew`는 `OSX`를 대상으로한 패키지 매니저이다.  
`homebrew`는 이것을 통해 설치할 소프트웨어에 제약을 두지 않는다.  
*python도 소프트웨어의 subset이다.*  

`brew`와 `pip`은 각각 설치경로가 다르다.  
`pip`을 통해 설치를 하면, `python interpreter가` 모듈을 찾는 곳에 설치를 한다.  

만약 `brew`를 통해 `python interpreter`를 설치했다면,  
`brew`를 통해 설치한 `python-package`가 외부에서도 사용가능할 가능성이 높다.

[내용 출처 :  Stack Overflow](https://stackoverflow.com/questions/32530506/is-there-a-difference-between-brew-install-and-pip-install)  

## pip vs pip3
`pip`은 `python2` 버전의 패키지 매니저이다.  
`pip3`는 `python3` 버전의 패키지 매니저이다. 