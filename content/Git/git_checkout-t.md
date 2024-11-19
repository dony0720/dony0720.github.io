---
emoji: 📝
title: git checkout -t
date: '2024-03-26 11:00:00'
author: 중석
tags: Git
categories: Git
---

## git checkout -t 에 대해서

아래와 같이 명령어를 진행하면 원격에 있는 브랜치를 로컬로 가져올 수 있다.  
(여기서 origin은 로컬내에 저장되어 있는 원격 저장소의 주소이다.)

```
git chekcout -t origin/원격에서 가져올 브랜치명
```

## fatal: 'origin/main' is not a commit and a branch 'main' cannot be created from it

프로젝트를 진행하면서 github의 feature/MonthChip 브랜치에서 pull을 받아올려고 했는데 위와 같은 에러가 발생 했다.

### 해결 방법

구글링 결과 후 아래와 같이 실행해서 해결할 수 있었다!

```
git  fetch  --all
```

참조 링크  
<https://shortcuts.tistory.com/27#google_vignette>

```toc

```
