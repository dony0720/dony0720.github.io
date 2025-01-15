---
emoji: 🔎
title: 프로그래머스 완주하지 못한 선수 Js
date: '2025-01-15 23:30:00'
author: 중석
tags: Algorithm
categories: Algorithm
---

## 문제 설명

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때,
완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

## 제한사항

마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.

## 입출력 예

| participant                                       | completion                               | return   |
| ------------------------------------------------- | ---------------------------------------- | -------- |
| ["leo", "kiki", "eden"]                           | ["eden", "kiki"]                         | "leo"    |
| ["marina", "josipa", "nikola", "vinko", "filipa"] | ["josipa", "filipa", "marina", "nikola"] | "vinko"  |
| ["mislav", "stanko", "mislav", "ana"]             | ["stanko", "ana", "mislav"]              | "mislav" |

## 입출력 예 설명

`예제 #1`  
"leo"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

`예제 #2`  
"vinko"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

`예제 #3`  
"mislav"는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

## mySolution

```js
function solution(participant, completion) {
  completion.forEach((item) => {
    if (participant.includes(item)) {
      const removeIndex = participant.indexOf(item);
      participant.splice(removeIndex, 1);
    }
  });
  return participant[0];
}
```

정확성 테스트는 통과했지만, 효율성 테스트 케이스에서 모두 탈락..!

## bestSolution

```js
participant.sort(); // [ 'ana', 'mislav', 'mislav', 'stanko' ]  참여 선수
completion.sort(); //  [ 'ana', 'mislav', 'stanko' ]  완주 선수

for (let i = 0; i < participant.length; i++) {
  if (participant[i] !== completion[i]) {
    return participant[i];
  }
}
```

- 참여선수와 완료선수의 값이 1개만 차이나는 점을 이용해 먼저 두 배열을 정렬 시킨다.
- 정렬된 두 배열을 for 반복문을 통해 각 인덱스의 값이 다른 구간을 찾는다.
- 값이 다르다는 것은 참여 선수가 완주 선수 리스트에 없다는걸 의미하기 때문에 해당 참여 선수를 반환한다.

```toc

```
