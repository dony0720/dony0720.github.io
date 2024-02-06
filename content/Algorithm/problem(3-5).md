---
emoji: 🔎
title: 프로그래머스 두 수의 연산값 비교하기 Js
date: '2024-02-05 17:00:00'
author: 중석 
tags: Algorithm
categories: Algorithm  
---

## 문제 설명
연산 ⊕는 두 정수에 대한 연산으로 두 정수를 붙여서 쓴 값을 반환합니다. 예를 들면 다음과 같습니다.

+ 12 ⊕ 3 = 123   
+ 3 ⊕ 12 = 312 
  
양의 정수 a와 b가 주어졌을 때, a ⊕ b와 2 * a * b 중 더 큰 값을 return하는 solution 함수를 완성해 주세요.

단, a ⊕ b와 2 * a * b가 같으면 a ⊕ b를 return 합니다.

##  제한사항
1 ≤ a, b < 10,000

## 입출력 예
|a|b|result|
|----|---|---|
| 2 | 91 | 364 |
| 91 | 2 | 912 |


## 입출력 예 설명

`입출력 예 #1`
+ a ⊕ b = 291 이고, 2 * a * b = 364 입니다. 둘 중 더 큰 값은 364 이므로 364를 return 합니다.

`입출력 예 #2`
+ a ⊕ b = 912 이고, 2 * a * b = 364 입니다. 둘 중 더 큰 값은 912 이므로 912를 return 합니다.

## solution.js 
```js
function solution(a, b) {
    let result1 = `${a}${b}`//string 
    let result2 = 2*a*b // number
    return +result1 >= result2 ? +result1 : result2;
} 
```

## 분석 
1. result1은 두 숫자를 ``을 이용해 문자열로 붙여 type이 string이고 result2은 type이 Number이다 
2. 두 값을 비교하기 위해서는 +을 이용해 result1을 숫자형으로 변환시킨다
3. 삼항연산자를 이용해 조건문이 참일 경우 숫자형으로 변환한 result1의 값을 반환하고    
거짓일 경우 result2의 값을 반환한다. 

```toc
```