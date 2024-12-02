---
emoji: 👨🏻‍💻
title: Day 11 함수 호이스팅, call by value & call by reference , 콜백함수
date: '2024-12-02 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 함수 호이스팅

함수 호이스팅이라 호출되는 시점에 함수의 선언이 없더라도 실행되는 메커니즘이다.
호이스팅은 인터프리터에 의하여 호출 시점 보다 늦게 선언된 함수는 상위로 이동 시키는
구문으로 일반 함수는 적용되지만 익명 함수는 호이스팅이 불가하다.

```js
/* 함수 선언 */
foo(); // "bar",
function foo() {
  // 호이스팅 되는 함수
  console.log('bar');
}

/* 함수 리터럴 표현식 */
baz(); // TypeError: baz is not a function
var baz = function () {
  console.log('bar2');
};
```

# Call by value

기본 자료형(Primitive Type, 원시 값)을 함수에 전달할 때, 값을 복사하여 전달한다. 단 본래의 값에 영향을 주지는 않는다. Call by Sharing도 같은 매커니즘이다.

```js
function func1(x) {
  x = 20; // 20
  console.log(`x : ${x}`); // 20
}

let num = 10;
func1(num);
console.log('num : ' + num);
```

- global : num = 10;
- stack : x = 10; -> 20; 함수내에서 x = 20을 만나면 20으로 변경됨!

# Call by Reference (참조에 의한 호출)

1. 참조 자료형(Reference Type)을 함수에 전달할 때, 참조값(메모리 주소)를 전달

## 객체

```
        obj  = 100번지주소
stack : user = 100번지주소


heap : {name:"홍길동"} 100번지
```

```js
function func2(obj) {
  // 참조형 객체
  obj.name = '김길동';
  console.log(obj); //{ name: '김길동' }
}

let user = { name: '홍길동' };
console.log(user); // { name: '홍길동' }
func2(user);
console.log(user); // { name: '김길동' }
```

## 배열

```js
let arr = [1, 2, 3];

function modifyArray(a) {
  a[0] = 99; // 같은 배열 참조
}

console.log(arr[0]); // 1
modifyArray(arr); // 배열 수정
console.log(arr[0]); // 99
```

```toc

```
