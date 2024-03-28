---
emoji: 🔎
title: 프로그래머스 수 조작하기 1 Js
date: '2024-03-27 14:30:00'
author: 중석 
tags: Algorithm
categories: Algorithm  
---
## 문제 설명
정수 n과 문자열 control이 주어집니다. control은 "w", "a", "s", "d"의 4개의 문자로 이루어져 있으며, control의 앞에서부터 순서대로 문자에 따라 n의 값을 바꿉니다.

+ "w" : n이 1 커집니다.
+ "s" : n이 1 작아집니다.
+ "d" : n이 10 커집니다.
+ "a" : n이 10 작아집니다.

위 규칙에 따라 n을 바꿨을 때 가장 마지막에 나오는 n의 값을 return 하는 solution 함수를 완성해 주세요.

## 제한사항
+ -100,000 ≤ n ≤ 100,000
+ 1 ≤ control의 길이 ≤ 100,000
    + control은 알파벳 소문자 "w", "a", "s", "d"로 이루어진 문자열입니다.

## 입출력 예 
|n|control|result|
|---|---|---|
| 0 | "wsdawsdassw" | -1|

## 입출력 예 설명
`입출력 예 #1`

+ 수 n은 control에 따라 다음과 같은 순서로 변하게 됩니다.
+ 0 → 1 → 0 → 10 → 0 → 1 → 0 → 10 → 0 → -1 → -2 → -1
+ 따라서 -1을 return 합니다.

## My solution.js
```js
function solution(n, control) {
  const controlAraay = [...control]
  controlAraay.map((item)=>{
      if(item === "w"){
          n += 1
      }
      else if (item === "s"){
          n -= 1 
      }
      else if (item === "d"){
          n += 10
      }
      else{
          n -=10;
      }
  })
    return n 
}
```

## Best solution.js 
```js
const operations = {
  w: (n) => n + 1,
  s: (n) => n - 1,
  d: (n) => n + 10,
  a: (n) => n - 10,
};

function solution(n, control) {
  return [...control].reduce((prev, op) => operations[op](prev), n);
}
```
1) operations 객체: 이 객체는 각각의 제어 문자에 대한 동작을 정의한다. 예를 들어, 'w'라는 문자가 주어지면 값을 증가시키는 함수가 정의되어 있다.
2) 처음 호출될 때는 초기값 n이 prev로 사용됩니다. 예를 들어, solution(0, 'wd')가 호출될 때, 초기값 0이 prev로 전달되고, 'w' 동작을 수행할 때는 prev가 0이 되고, 'd' 동작을 수행할 때는 이전 단계에서의 결과값이 1인 1이 prev로 전달 된다.
3) operations [op] (prev) 부분은 operations 객체에서 현재 제어 문자 op에 해당하는 함수를 호출하고, 그 함수에 이전 단계에서의 결과값인 prev를 operation 객체에 전달하여 현재 단계에서의 결과를 계산하는 것입니다.