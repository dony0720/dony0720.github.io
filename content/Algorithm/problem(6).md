---
emoji: 📝
title: 프로그래머스 덧셈식 출력하기 Js
date: '2024-01-22 12:00:00'
author: 중석
tags: Algorithm
categories: Algorithm
---

# 문제 설명

두 정수 a, b가 주어질 때 다음과 같은 형태의 계산식을 출력하는 코드를 작성해 보세요
```
a + b = c
```

## 제한사항
```
1 ≤ a, b ≤ 100
```

## 입출력 예

`입력#1`
```
4 5 
```
`출력 #1`
```
4 + 5 = 9
```

## solution.js 
```js 
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let input = [];

rl.on('line', function (line) {
    input = line.split(' ');
}).on('close', function () {
    const a = input[0]
    const b = input[1]
    console.log(`${a} + ${b} = ${Number(a)+Number(b)}`);
});
```

## 분석 

```js 
input = line.split(' ');
```
한줄로 입력 받은 값을 한글자씩 구분해 input 변수에 저장한다. 

```js
const a = input[0]
const b = input[1]
console.log(`${a} + ${b} = ${Number(a)+Number(b)}`);
```
```toc
```