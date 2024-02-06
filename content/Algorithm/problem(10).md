---
emoji: 🔎
title: 프로그래머스 더 크게 합치기 Js  
date: '2024-02-05 16:50:00'
author: 중석 
tags: Algorithm
categories: Algorithm  
---

## 문제 설명 
연산 ⊕는 두 정수에 대한 연산으로 두 정수를 붙여서 쓴 값을 반환합니다. 예를 들면 다음과 같습니다.

+ 12 ⊕ 3 = 123   
+ 3 ⊕ 12 = 312   

양의 정수 a와 b가 주어졌을 때, a ⊕ b와 b ⊕ a 중 더 큰 값을 return 하는 solution 함수를 완성해 주세요.

단, a ⊕ b와 b ⊕ a가 같다면 a ⊕ b를 return 합니다.

## 제한사항
1 ≤ a, b < 10,000

## 입출력 예

|a|b|result|
|----|---|---|
| 9 | 91 | 991 |
| 89 | 8 | 898 |

## 입출력 예 설명

`입출력 예 #1` 
+ a ⊕ b = 991 이고, b ⊕ a = 919 입니다. 둘 중 더 큰 값은 991 이므로 991을 return 합니다.

`입출력 예 #2`
+ a ⊕ b = 898 이고, b ⊕ a = 889 입니다. 둘 중 더 큰 값은 898 이므로 898을 return 합니다.


## solution.js
```js
function solution(a, b) {
    let result1 = `${a}${b}`
    let result2 = `${b}${a}`

    if(+result1 >= +result2){
        return +result1 
    }
    else if (+result1 < +result2){
        return +result2
    }
}
```

## 분석 
```js
let result1 = `${a}${b}`
let result2 = `${b}${a}`
```
정수 a,b를 ``(백틱)을 이용해 문자열로 합친 결과를 result1, result2 에 저장한다. 

```js
if(+result1 >= +result2){
    return +result1 
}
else if (+result1 < +result2){
    return +result2
}
```
1. result1이 result2 보다 >= 경우 + 사용해 result1의 값을 숫자형으로 변환해 반환한다. 
2. result1이 result2 보다 < 경우 + 사용해 result2의 값을 숫자형으로 변환해 반환한다. 

```toc
```