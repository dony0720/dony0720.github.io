---
emoji: 🔎
title: 프로그래머스 공배수 Js
date: '2024-02-06 16:10:00'
author: 중석 
tags: Algorithm
categories: Algorithm  
---

## 문제 설명
정수 number와 n, m이 주어집니다. number가 n의 배수이면서 m의 배수이면 1을    
아니라면 0을 return하도록 solution 함수를 완성해주세요.

## 제한사항
+ 10 ≤ number ≤ 100
+ 2 ≤ n, m < 10 

## 입출력 예 
|num|n|m|result|
|---|---|---|---|
| 98 | 2 | 1 | 1 |
| 34 | 3 | 0 | 0 |   

## 입출력 예 설명
`입출력 예 #1`

+ 60은 2의 배수이면서 3의 배수이기 때문에 1을 return합니다.

`입출력 예 #2`

+ 55는 5의 배수이지만 10의 배수가 아니기 때문에 0을 return합니다.

## solution.js 
```js
function solution(number, n, m) {
    return number%n===0 && number%m===0 ? 1 : 0
} 
```

## 분석 
삼항 연산자를 이용해 numebr를 n과 m 으로 각각 나누었을때의 값이 0이면 조건문이 참이기 때문에 1을 return한다. 

```toc
```