---
emoji: 📝
title: 프로그래머스 코테 연습문제 (4)
date: '2024-01-22 11:35:00'
author: 중석
tags: Algorithm
categories: Algorithm
---

# 대소문자 바꿔서 출력하기

## 문제 설명 
영어 알파벳으로 이루어진 문자열 str이 주어집니다.    
각 알파벳을 대문자는 소문자로 소문자는 대문자로 변환해서 출력하는 코드를 작성해 보세요.

## 제한 사항 
+ 1 ≤ str의 길이 ≤ 20
    + str은 알파벳으로 이루어진 문자열입니다.

## 입출력 예 
`입력 #1`
```
aBcDeFg
```

`출력 #1`
```
AbCdEfG
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
    str = input[0].split('');
    str.forEach((value, index) => {
        if (value === value.toUpperCase()) {
            str[index] = value.toLowerCase();
        } else {
            str[index] = value.toUpperCase();
        }
    });
    console.log(str.join(''));
});
```

## 분석 
```js
str = input[0].split('');
str.forEach((value, index) => {
    if (value === value.toUpperCase()) {
        str[index] = value.toLowerCase();
    } else {
        str[index] = value.toUpperCase();
    }
});
console.log(str.join(''));
```
1) str의 첫번째 인덱스값을 한글자씩 분리해서 str = [a,B,c,D,e,F,g]로 만들었다 
2) forEach 반복문을 사용해 각 인덱스의 값이 대문자인지 소문자인지 구분한다. 
   + toUpperCase()를 사용해 해당 값이 대문자이면 toLowerCase()를 사용해 소문자로 변환한다.    
   + toLowerCase()를 사용해 해당 값이 소문자이면 toUpperCase()를 사용해 대문자로 변환한다. 
3) 변환된 글자들은 str 배열에 저장되어 있고 str.join('')을 이용해    
   각 인덱스에 저장된 글자를 한번에 합쳐서 출력한다. 

   ```toc
   ```