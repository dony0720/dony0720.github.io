---
emoji: 👨🏻‍💻
title: Day 8 JS변수, var 호이스팅 개념과 이슈
date: '2024-11-27 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 자바스크ㄹ비트 작성 유형

## internal(내부) 방식

- 인라인 방식으로 HTML 속성 내부에 짧게 작성하는 방법
- 아주 짧게 쓰는 것을 권장하고 주로 함수 호출을 통해 문자를 늘려서 활용

```html
<button onclick="alert(`인라인 방식`)">alert 버튼</button>
```

## External(외부)에서 호출하는 방법

- 단, js 코드 특성상 외부에서만 로드하는 것은 불가능해 internal 방식과 섞어서 사용한다
- script 태그 안에 js 외부파일 경로를 src에 입력 해주면 된다

```html
<script src="01_external.js"></script>
```

## 변수 정의 및 키워드

변수: JS에서 값을 저장하는 공간이다. 쉽게 말해 빈 박스 => 변수 , 박스 안에 들어있는 물건 => 값 이라고 생각해도 좋다

변수 선언 키워드

- var : ES6 이전 문법에서 사용된 키워드지만 ES6 이후로는 잘 쓰지 않음 ex) var value = 10;
- let(ES6) : 블록 스코프를 가지는 변수로 완벽한 지역변수 ex) let value = 10;
- const(ES6) : 상수로 선언시 활용, 값이 한번 정해지면 변경 불가! ex) const = 10;

## 문자열 + 숫자 혼합 사용

- 문제점: 문자열 + 숫자 = 문자, 문자/숫자 혼합되는 경우 우선순위 이슈가 발생할 수 있음
- 해결법: 괄호를 사용해라!

```js
let str1 = 'hello '; // 더블 쿼테이션으로 문자열 표기 가능
let num1 = 20;

console.log(str1 + num1 + 1000); // => 출력값: hello 201000
console.log(str1 + (num1 + 1000)); // 출력값: hello 1020
```

### 분석

console.log(str1 + num1 + 1000)의 동작 과정

1. str1(문자열) + num1 (숫자)는 숫자를 문자열로 변환 => 문자열 hello 20을 출력하게 된다
2. hello 20(문자열) + 1000(숫자) => 문자열 hello 201000을 출력하게 된다

console.log(str1 + (num1 + 1000)) , 괄호 사용

1. ( )를 사용함으로 우선순위를 정해준다
2. 우선순위로 인해 num1(숫자) + 1000(숫자) => 1020을 출력한다
3. str1(문자열) + 1020(숫자) => hello 1020을 출력한다

## var 호이스팅 및 이슈

- 변수 선언이 함수 또는 전역 코드의 상단에 이동하는 것을 "호이스팅(hoisting)"이라 말한다.

```js
// 실제 코드
bla = 2;
var bla;
console.log(2);

// 호이스팅 적용된 코드
var bla;
bla = 2;
console.log(2);
```

## 호이스팅 이슈

- var는 JavaScript에서 사실상 전역적인 변수 활용의 키워드로 이해 하면 편하다.

```js
// 전역
console.log(name); // undefined 원래는 ReferenceError가 발생해야됨
var name = 'Mike';
console.log(name); // "Mike"
```

위 코드를 호이스팅의 개념으로 정리하면 아래와 같다

```js
var name; //→ 선언된 변수가 최상위로 올라왔다
console.log(name); // name이란 변수가 선언은 됐지만 값이 없어 undefined를 출력한다
name = 'Mike'; //→ 그러나 값은 올라가지 못한다. 따라서 값은 할당해주어야 한다
console.log(name); // Mike란 값이 할당되어 Mike를 출력한다
```

```toc

```
