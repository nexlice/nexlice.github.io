---
title: Git Commands
tags: 
 - git
 - restore
 - reset
description: Learn about basic git commands!
---

필자는 지인 추천으로 `fork` 서드파티 앱을 사용한다.  
하지만 때에 따라서 직접 `terminal`에서 `git`명령어를 사용해야하는데, 헷갈리는 부분을 정리해보았다.   

# restore
```bash
git restore <파일명>
```
커밋되지 않은 local repo 의 변경 사항을 취소할 수 있다.  

# reset
```bash
git reset
```
리모트에 업로드 되지 않고 로컬에만 커밋해 놓은 기록;커밋 을 취소할 수 있다.  
`git reset HEAD^` 명령어로 가장 최신의 커밋을 취소할 수 있다.  

참고로 HEAD3은 HEAD^^^와 같다.  
`HEAD^`은 `HEAD~1` 와 동일하다.  
