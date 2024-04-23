---
emoji: 🔎
title: 프로그래머스 카운트 업 Js
date: '2024-04-23 22:55:00'
author: 중석
tags: Algorithm
categories: Algorithm
---

## 문제 설명

정수 start_num와 end_num가 주어질 때, start_num부터 end_num까지의 숫자를 차례로 담은 리스트를 return하도록 solution 함수를 완성해주세요.

## 제한사항

- 0 ≤ start_num ≤ end_num ≤ 50

## 입출력 예

| start_num | end_num | result                    |
| --------- | ------- | ------------------------- |
| 3         | 10      | [3, 4, 5, 6, 7, 8, 9, 10] |

## 입출력 예 설명

입출력 예 #1

- 3부터 10까지의 숫자들을 담은 리스트 [3, 4, 5, 6, 7, 8, 9, 10]를 return합니다.

## solution.js

```js
function solution(start, end) {
  return Array.from({ length: end - start + 1 }, () => {
    return start++;
  });
}
```

## 분석

1. Array.from() 메서드를 사용하여 새로운 배열을 생성합니다. 이 배열은 start부터 end까지의 연속된 숫자를 포함한다. `{length: end-start+1}`을 전달하여 새 배열의 길이를 설정한다.

2. 두번째 인수로는 매핑 함수를 받아서 배열의 각 요소를 `start`부터 시작하여 1씩 증가하는 값으로 반환한다.

```toc

```
