---
emoji: 🧢
title: Git에 대해서 (1) 
date: '2023-03-30 10:30:00'
author: Js 
tags: Git
categories: Git 
---

# 버전관리 

## 버전 생성 

1. `working Tree`: 파일을 수정하는 곳 

2. `Staging Area`: 곧 커밋할 파일에 대한 정보를 저장하는 곳

3. `Repository`: 만들어진 버전을 저장하는 곳이다. 즉, 우리가 저장소라가고 불리는 곳이다. 

4. `Untracked files`: 한번도 버전 관리하지 않은 파일 

5. `git add`: 버전을 만들기 위해 파일을 Staging Area 올린다. 

6. `git commit  -m ""` 
    
    + -m 은 메세지의 약자이고, 뒤에 ""안에 공유할 메시지 내용을 적어주시면 됩니다.
    
    + 파일이 Repository로 가게 된다. 즉, 버전을 생성한다.   

7. `git -a`
    + add 되야하는 파일이 있거나 delete 된 파일이 있는 상태 일때, 알아서 add 가 진행된 후 commit 이 된다.
    
    + 단 최초 한번의 add가 되어있어야 사용할 수  있다.
 
8. `git commit -am""`
    
    + `git -a`에서 적고자하는 메시지를 넣는걸 추가한 것이다.

    + `git -a`와 똑같이 add가 진행된 후에 자동으로 commit이 된다.

8. `git commit` 과 git `push`의 차이점

    + `git commit`은 지역저장소(local Repository)에 변경사항을 기록한다.  
    
    + `git push`는 커밋된 변경사항을 원격저장소(remote Repository)에 업로드한다. 
    
    + 즉 `git commit`은 지역저장소 내에서만 이루어진다. 하지만 `git push`는 지역저장소 -> 원격저장소로 작용한다.


## 여러개의 파일을 하나의 버전으로 만들기 

1. 하나의 버전으로 만들고자 하는 파일들을 `git add`를 통해서 `Staging Area`에 올린다,

2. `git commit`: Repository를 생성한다. 

3. `git log - stat` 을 통해  각각의 버전마다 어떤 파일이 포함되어 있는지, 각각의 파일에 변경사항을 확인할 수 있다. 

## 버전간의 차이점 비교 

1. `git - diff`: 이전 버전과 현재 버전의 비교를 할 수 있다.

2. `git log -p`: 각 버전의 차이점을 볼 수 있다.

## checkout을 통한 버전 돌아가기 

1. `git checkout(커밋된 데이터 버전의 고유 번호)`
    
    + 돌아가고 싶은 버전으로 가게 되어 내용을 확인할 수 있다.

    + checkout한 버전의 파일을 수정하게 되면 새로운 branch를 생성한다. 

2. `git checkout master`: 최신상태의 버전으로 돌아가싶을때

## 버전 삭제 

`git reset --hard 돌아갈 버전의 고유 번호` : 돌아간 커밋 이후의 변경 이력은 모두 삭제합니다.

```   

git commit -m "1"
git commit -m "2"
git commit -m "3"

git reset --hard [1번commit의 고유 번호]
git push

```
위 코드 진행시 2,3번의 변경이력, 변경내용은 사라지게 된다. 

## 되돌리기 

1. `git revert 커밋된 데이터의 고유 번호`

+ A - 현재 버전, B - 이전 버전 이라고 가정하자 git revert를 진행하게 되면 B의 내용을 가진 새로운 C 버전이 생성되고 
  C-> A-> B 의 순서로 생성되어진 것을 확인할 수 있다.  

+ 만약 A->B->C->D 의 순서로 버전이 있고 현재 버전이 A라고 가정한다.
  D버전으로 revert를 진행하고 싶을때는 바로 git revert C를 진행하게 되면 충돌이 발생하게된다.  
  그래서 순차적으로 A-> B-> C의 순서로 revert를 진해해야 한다. 


## 🔥 즉, 버전관리의 핵심은 비교라고 말할 수 있습니다!!

```toc

```