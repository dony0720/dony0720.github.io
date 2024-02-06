---
emoji: 🔎
title: 프로그래머스 문자열 돌리기 Js  
date: '2024-02-05 16:40:00'
author: 중석 
tags: Algorithm
categories: Algorithm  
---

## 문제설명 
문자열 str이 주어집니다.   
문자열을 시계방향으로 90도 돌려서 아래 입출력 예와 같이 출력하는 코드를 작성해 보세요.

## 제한사항
1 ≤ str의 길이 ≤ 10

## 입출력 예
`입력#1`
```
abcde
```

`출력#1`
```
a
b
c
d
e
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
    input = [line];
}).on('close',function(){
    str = input[0];
    [...str].forEach((item)=> console.log(item))
}); 
```

## 분석 

```js
 [...str].forEach((item)=> console.log(item))
```
1. str을 전개구문을 이용해 [ 'a', 'b', 'c', 'd', 'e' ]의 배열을 만든다. 
2. forEach 구문을 통해 각 배열에 있는 값을 console.log( )를 통해 출력한다.

```toc
```