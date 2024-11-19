---
emoji: 🔎
title: 프로그래머스 카운트 업 Js
date: '2024-04-22 23:00:00'
author: 중석
tags: Algorithm
categories: Algorithm
---

## 문제 설명

모든 자연수 x에 대해서 현재 값이 x이면 x가 짝수일 때는 2로 나누고, x가 홀수일 때는 3 \* x + 1로 바꾸는 계산을 계속해서 반복하면 언젠가는 반드시 x가 1이 되는지 묻는 문제를 콜라츠 문제라고 부릅니다.

그리고 위 과정에서 거쳐간 모든 수를 기록한 수열을 콜라츠 수열이라고 부릅니다.

계산 결과 1,000 보다 작거나 같은 수에 대해서는 전부 언젠가 1에 도달한다는 것이 알려져 있습니다.

임의의 1,000 보다 작거나 같은 양의 정수 n이 주어질 때 초기값이 n인 콜라츠 수열을 return 하는 solution 함수를 완성해 주세요.

## 제한사항

- 1 ≤ n ≤ 1,000

## 입출력 예

| n   | result                  |
| --- | ----------------------- |
| 10  | [10, 5, 16, 8, 4, 2, 1] |

## 입출력 예 설명

입출력 예 #1

순서대로 연산한 결과를 표로 만들면 다음과 같습니다.

| 연산 횟수 | x   | 홀짝 여부 |
| --------- | --- | --------- |
| 0         | 10  | 짝수      |
| 1         | 5   | 홀수      |
| 2         | 16  | 짝수      |
| 3         | 8   | 짝수      |
| 4         | 4   | 짝수      |
| 5         | 2   | 짝수      |
| 6         | 1   | 홀수      |

## My solution.js

```js
function solution(n) {
  var answer = [];
  answer.push(n);
  while (n !== 1) {
    if (n % 2 === 0) {
      n = n / 2;
      answer.push(n);
    } else {
      n = 3 * n + 1;
      answer.push(n);
    }
  }
  return answer;
}
```

## Best solution.js

```js
function solution(n, arr = []) {
  arr.push(n);
  if (n === 1) return arr;
  if (n % 2 === 0) return solution(n / 2, arr);
  return solution(3 * n + 1, arr);
}
```

## Best solution.js 분석

1. n이 1일 경우 현재의 배열을 바로 반환한다.
2. n이 짝수일 경우에는 함수가 자신을 다시 호출하는 재귀함수를 사용해 `n/2`의 값과 arr을 인자로 전달한다.
3. 그리고 이 두 경우를 제외한 홀수일 경우에는 마찬가지로 재귀함수를 사용해 `3*n+1`의 값과 arr을 인자로 전달한다.

```toc

```
