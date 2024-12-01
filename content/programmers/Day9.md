---
emoji: 👨🏻‍💻
title: Day 9 동적 타이핑 개념, Symbol, Truthy & Falsy
date: '2024-11-28 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 동적 타이핑 개념

JavaScript의 변수 선언 시 type(자료형)을 선언하지 않아도 되며, 향후 값이 대입(assign) 되는 순간
type이 결정되는 동적 타이핑(Dynamic Typing) 메커니즘을 활용한다.

단, type이 없는 것이 아니라 나중에 결정되는 메커니즘으로 type이 존재한다!

Type 종류 : 원시형(Number, String, Boolean ... ), Object(객체, 배열, 함수 등)

```js
let name;
name = 'John';
name = 120; // 문제 없이 type 변경됨!
console.log(name); // => 120 출력
```

```java
String name;
name = "John";
name = 120; // 컴파일 에러 발생!
```

java에서는 한번 정해진 type은 변경이 불가하지만 js에서는 변수에 어떤 type의 값이 들어와도 변경이 가능하다!

# Symbol (심벌)

ES6에서 새롭게 도입된 기본 자료형 중 하나로, 고유하고 변경 불가능한 값을 생성이 가능하다.
주로 객체의 속성키로 활용 가능하며 충돌 가능성 없는 고유 식별자를 만들기 위해도 활용 됨

```js
const symbol1 = Symbol('my symbol');
const symbol2 = Symbol('my symbol');
console.log(symbol1 === symbol2); // false

const id1 = Symbol('id');
const id2 = Symbol('id');
const obj = {
  [id1]: 'value1',
  [id2]: 'value2',
};

console.log(obj[id1]); // "value1"
console.log(obj[id2]); // "value2"
```

# Truthy & Falsy 값

## Truthy

참 같은 값(Truthy)인 값이란 불리언을 기대하는 문맥에서 true로 평가되는 값이다.
따로 거짓 같은 값으로 정의된 값이 아니면 모두 참 같은 값으로 평가된다

```js
if (true)
if ({})
if ([])
if (42)
if ("0")
if ("false")
if (new Date())
if (-42)
if (12n)
if (3.14)
if (-3.14)
if (Infinity)
if (-Infinity)

```

- 위 예시는 javaScript에서 true로 판정되는 값들이다

## Falsy

반대로 Falsy 값은 Boolean 문맥에서 false로 평가되는 값이다

```js
if(false)
if(null)
if(undefined)
if(0)
if(NaN)
if('')
```

```toc

```
