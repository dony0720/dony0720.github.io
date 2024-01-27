---
emoji: 📝
title: 프로그래머스 코테 연습문제 (2)
date: '2024-01-17 11:10:00'
author: 중석
tags: Algorithm
categories: Algorithm
---

# a와 b 출력하기

## 문제설명

정수 `a`와 `b`가 주어집니다. 각 수를 입력받아 입출력 예와 같은 형식으로 출력하는 코드를 작성해 보세요.

## 제한사항

- -100,000 ≤ a, b ≤ 100,000

## 입출력 예

입력 # 1

```
4 5
```

출력 #1

```
a = 4
b = 5
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
  console.log(`a = ${Number(input[0])}`);
  console.log(`b = ${Number(input[1])}`);
});
```

`입력 부분`
1) 한줄씩 입력받은 값을 공백을 기준으로 구분해서 input 배열에 선언한다.

`출력 부분`
1) 백틱을 사용해 문자열과 input 배열에 담겨있는 각 인덱스의 값을 한번에 출력한다 
   
```toc
```