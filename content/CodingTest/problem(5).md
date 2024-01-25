---
emoji: 📝
title: 프로그래머스 코테 연습문제 (5)
date: '2024-01-22 11:45:00'
author: 중석
tags: Algorithm
categories: Algorithm
---

# 특수문자 출력하기

## 문제 설명

다음과 같이 출력하도록 코드를 작성해 주세요.

## 출력 예시 
```
!@#$%^&*(\'"<>?:;
```
## solution.js 
```js
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('close', function () {
    const speacial_str = `!@#$%^&*(\\\'"<>?:;`
    console.log(speacial_str)
});
```

## 분석 
```js
const speacial_str = `!@#$%^&*(\\\'"<>?:;`
console.log(speacial_str)
```

1) 자바스크립트 내에서는 특수문자를 처리하기 위해서는 백슬러시를 이용한 특수문자 표기 방법(=escape)이 있다.     
2) speacial_str에서는 문자열 표현을 위해 기존 따옴표에서 백틱(`)을 사용했다.   
3) \\' escape 문자로 인해 사라지게 될 백슬래시를 보충하기 위해  
4) escape 문자 앞에 백슬래시(\\)를 하나 더 추가하여 해결하였다.

## eascape 문자 

|특수문자|출력 형태 및 설명 |영문표기|
|----|---|---|
| \\' | ' | single quote |
| \\" | " | double quote |
| \\\ | \ | backslash |
|\n| 커서를 다음 줄로 이동| new line |
|\r| 커서를 해당 줄 처음으로 이동 | carriage return |
|\t| 커서를 탭 만큼 이동 | 	tab |
|\b| 백스페이스(←)와 동일하게 작동 | backspace |
|\f| 커서를 다음 페이지로 이동 (용지 넘김 문자) | form feed |

```toc
```