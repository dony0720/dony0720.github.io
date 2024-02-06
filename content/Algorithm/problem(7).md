---
emoji: 🔎
title: 프로그래머스 문자열 붙여서 출력하기 Js  
date: '2024-02-05 16:30:00'
author: 중석 
tags: Algorithm
categories: Algorithm  
---

## 문제 설명 
두 개의 문자열 str1, str2가 공백으로 구분되어 입력으로 주어집니다.  
입출력 예와 같이 str1과 str2을 이어서 출력하는 코드를 작성해 보세요.

## 제한사항
1 ≤ str1, str2의 길이 ≤ 10

## 입출력 예
`입력 #1`
```
apple pen
```

`출력 #1`
```
applepen
``` 

`입력 #2`
```
Hello World!
```

`출력 #2`
```
HelloWorld!
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
    console.log(input.join('')) 
});
``` 

## 분석 
join(' ')을 이용해 띄어진 두 문자열을 합쳐 출력한다. 

```toc
```