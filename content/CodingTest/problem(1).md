---
emoji: 📝
title: 프로그래머스 코테 연습문제 (1) 
date: '2024-01-16 16:30:00'
author: 중석 
tags: algorithm
categories: algorithm  
---


# 문자열 출력하기 

## 문제설명 
문자열 `str`이 주어질 때, `str`을 출력하는 코드를 작성해 보세요.

## 제한사항
+ 1 ≤ str의 길이 ≤ 1,000,000
+ str에는 공백이 없으며, 첫째 줄에 한 줄로만 주어집니다.

## 입출력 예 

입력 #1
```
HelloWorld!
```

출력 #1
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
    input = [line];
}).on('close',function(){
    str = input[0];
    console.log(str)
});
```

### readline 모듈  
+ readline 모듈은 JavaScript에 내장된 모듈 
+ 자바스크립트에서는 readline 모듈을 이용하면 콘솔을 통해 값을 입력받을 수 있다.
+ readline모듈은 사용자의 입력을 console.log로 출력할 수 있도록 해주는 역할을 한다.

### 모듈 불러오기 
```
const readline = require("readline")
```

### readline 모듈을 이용해 입출력을 위한 인터페이스 객체 만들기
```js
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});
```
+ 정의한 변수를 이용해 readline 인터페이스 객체를 하나 만들어줍니다.
+ readline interface 객체를 이용해 콘솔에서 표준 입출력을 처리할 수 있습니다. 
+ creacteInterface()메서드를 이용해 객체를 만들고, rl 변수에 저장해줍니다.

### on 메소드 
+ 생성한 변수 rl 객체로 입출력과 관련된 여러 이벤트 처리를 할 수 있습니다. 
+ 예를 들어 사용자가 콘솔에 입력을 넣는 것과 같은 이벤트가 있습니다. 
+ on메소드를 이용하면 이벤트가 발생할 때 실행할 동작을 지정할 수 있습니다.

### line 이벤트 
+ line이벤트는 입력 스트림이 줄 끝 입력 (\ n, \ r 또는 \ r \ n)을 수신 할 때마다 발생되는데,    
  줄 끝 입력은 보통 사용자가 Enter 또는 Return을 누를 때 발생한다. 


### rl 변수
```js
rl.on('line', function (line) { // 입력 부분 
    input = [line];
}).on('close',function(){ // 출력 부분 
    str = input[0];
    console.log(str)
});
```
`입력 부분`    
1) 한줄씩 입력 받은 후 line에 값이 저장된다.
2) input 배열에 line을 저장한다. 

`출력 부분`
1) 입력이 끝난후에 아래 코드가 동작하게 된다. 
2) input 배열에 저장되어 있는 인덱스 0번을 str이라는 변수에 선언한다.
3) console.log 를 통해 str에 저장된 문자열을 출력한다. 