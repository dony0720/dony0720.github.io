---
emoji: 🔎
title: 프로그래머스 마지막 두 원소 Js
date: '2024-03-28 14:00:00'
author: 중석 
tags: Algorithm
categories: Algorithm  
---

## 문제 설명 
정수 리스트 num_list가 주어질 때, 마지막 원소가 그전 원소보다 크면 마지막 원소에서 그전 원소를 뺀 값을 마지막 원소가 그전 원소보다 크지 않다면 마지막 원소를 두 배한 값을 추가하여 return하도록 solution 함수를 완성해주세요.

## 제한 사항 
+ 2 ≤ num_list의 길이 ≤ 10
+ 1 ≤ num_list의 원소 ≤ 9

## 입출력 예 
|num_list|result|
|---|---|
| [2, 1, 6] | [2, 1, 6, 5] |
| [5, 2, 1, 7, 5] | [5, 2, 1, 7, 5, 10] |

## 입출력 예 설명
`입출력 예 #1`

마지막 원소인 6이 그전 원소인 1보다 크기 때문에 6 - 1인 5를 추가해 return합니다.

`입출력 예 #2`

마지막 원소인 5가 그전 원소인 7보다 크지 않기 때문에 5의 두 배인 10을 추가해 return합니다.

## My solution.js
```js 
function solution(num_list) {
    const last = num_list[num_list.length - 1] // 마지막 원소 
    const lastPrev = num_list[num_list.length - 2] // 마지막 전 원소 
    if( last > lastPrev ) {
        num_list.push(last-lastPrev)
        return num_list
    }
    else {
        num_list.push(2*last)
        return num_list
    }
}
```

## Best solution.js
내 풀이보다 더 깔끔한 풀이가 있길래 가져와봤다!

```js
function solution(num_list) {
    const [a, b] = [...num_list].reverse();
    return [...num_list, a > b ? (a-b):a*2];
}
```

   
1) 입력 예제 1번을 통해 설명하면 [...num_list]를 통해서 원본 배열을 그대로 유지하면서 새로운 배열을 만든다.
2) reverse( ) 메서드를 통해서 배열 순서가 [6, 1, 2]로 바뀌고 구조분해할당으로 a = 6, b = 1 값이 할당된다. 
3) 삼항연사자를 이용해 조건문 결과에 따른 값을 배열의 마지막 값에 추가한다. 

```toc
```