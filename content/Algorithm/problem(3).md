---
emoji: 📝
title: 프로그래머스 코테 연습문제 (3)
date: '2024-01-17 11:20:00'
author: 중석
tags: Algorithm
categories: Algorithm
---

# 문자열 반복해서 출력하기

## 문제설명

- 문자열 str과 정수 n이 주어집니다.
- str이 n번 반복된 문자열을 만들어 출력하는 코드를 작성해 보세요.

## 제한사항

- 1 ≤ str의 길이 ≤ 10
- 1 ≤ n ≤ 5

## 입출력 예

입력 #1  

```
string 5
```

출력 #1

```
stringstringstringstringstring
```

## solution.js

```js
const readline = require('readline');
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

let input = [];

rl.on('line', function (line) {
  input = line.split(' ');
}).on('close', function () {
  str = input[0];
  n = Number(input[1]);
  console.log(str.repeat(n));
});
```
`입력 부분`
1) 한줄씩 입력받은 값을 공백을 기준으로 구분해서 input 배열에 선언한다.

`출력 부분`
1) input의 인덱스 0에 있는 문자열은 str 변수에 선언하고    
인덱스 1에 있는 문자열은 Number를 통해 숫자형으로 변환후 n 변수에 선언한다. 
2) repeat() 메서드 사용 
+ repeat() 메서드는 문자열을 주어진 횟수 만큼 반복해 붙이 문자열을 반환한다.
+ str에 저장된 문자열을 repeat() 메서는들 사용해 n만큼 반복하면 된다. 

```toc
```