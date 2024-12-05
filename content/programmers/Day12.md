---
emoji: 👨🏻‍💻
title: Day 12 객체
date: '2024-12-03 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 객체 생성

## 객체 리터럴

가장 기본적인 객체 생성법이다

```js
let obj = {
  // 속성 값 위로 선언
  name: '홍길동',
  age: 19,
  hobby: ['축구', '농구', '영화보기', '게임'],

  // 일반 메서드 표현법
  sayHello: function () {
    console.log(`안녕하세요? ${this.name} 입니다.`);
  },
  // ES6 이후 단축된 메서드 표현
  sayBye() {
    console.log(`안녕히 계세요. ${this.name}은 갑니다.`);
  },
};
```

## 생성자 함수

고전(ES5이전)부터 재사용이 필요한 객체를 설계하는 방법으로 함수의 첫 글자를 대문자로 선언하여 활용
ES6 이후에는 Class 문법이 생겼지만 여전히 객체 선언 시 표준적으로 활용 되는 문법

- new : 생성자 함수를 생성하는 키워드로 새로운 Heap 메모리 공간에
- this : 해당 블록에 해당되는 객체 자신(this)을 가르치는 키워드

### 인스턴스

생성자 함수를 통해 생성된 객체를 인스턴스(instance)라 한다.

```js
function Person(name, age, address) {
  this.name = name;
  this.age = age;
  this.address = address;
}
let person1 = new Person('홍길동', 21, '서울시 강남구'); // new = 생성자로 객체 생성하는 방법,
let person2 = new Person('최길동', 41, '서울시 서초구');
let person3 = new Person('김길순', 31, '서울시 구로구');
```

위 코드에서 Person은 생성자 함수 쉽게 말해 프레임이고 아래 선언된 person 1부터 3은 전달된 인자가 객체 프로퍼티에 값을 지정한다

## Object 생성자

```js
// Object 및 다른 Object Wrapper를 통해 다양한 객체를 생성
const person = new Object();

// 프로퍼티 추가하는 방법
person.name = '홍길동';
person.sayHello = function () {
  console.log('Hello ' + this.name);
};
console.log(person);
person.sayHello();
```

### Object Wrapper

```js
let strObj = new String('text');
let numObj = new Number(100);
let boolObj = new Boolean('true');
let funcObj = new Function('a, b', 'return a + b;');
let arrayObj = new Array(1, 2, 3);
let dateObj = new Date();
```

```
출력값

[String: 'text']
[Number: 100]
[Boolean: true]
[Function: anonymous]
[ 1, 2, 3 ]
2024-12-03T08:03:10.162Z
```

### Object create( )

1. 프로토타입을 명시적으로 설정하면서 객체를 생성하는 방법
2. 빈객체를 만들기보단 상속이나 복제 용도로 활용

```js
let myObj1 = {
  a: 10,
  b: 20,
  plus() {
    return this.a + this.b;
  },
};

let myObj2 = Object.create(myObj1);
```

복제되어 새로운 heap에 myObj2 만들어진다. myObj1도 heap에 존재하기때문에 myObj2d와 myObj1은 각각 별도의 메모리를 차지한다. 하지만 myObj2는 myObj1의 프로토타입은 참조한다. (깊은 복사)

```js
myObj2.a = 100;
myObj2.b = 200;
```

myObj2에 프로퍼티를 추가하면, 이는 myObj1과 상관없이 myObj2만의 고유 데이터가 된다.

## 생성자 함수에서의 this

```js
function Calc(x, y) {
  this.x = x;
  this.y = y;
  this.plus = function () {
    return this.x + this.y;
  };
  this.minus = function () {
    return this.x - this.y;
  };
  this.multiple = function () {
    return this.x * this.y;
  };
  this.divide = function () {
    return this.x / this.y;
  };
}
```

동작 방식은 아래와 같다

1. 빈 객체 생성 및 this 바인딩

   - 생성자 함수의 코드가 실행되기 전 빈 객체가 생성된다. 이 빈 객체가 생성자 함수가 새로 생성하는 객체이다. 이후 생성자 함수 내에서 사용되는 this는 이 빈 객체를 가리킨다. 그리고 생성된 빈 객체는 생성자 함수의 prototype 프로퍼티가 가리키는 객체를 자신의 프로토타입 객체로 설정한다.

2. this를 통한 프로퍼티 생성

   - 생성된 빈 객체에 this를 사용하여 동적으로 프로퍼티나 메소드를 생성할 수 있다. this는 새로 생성된 객체를 가리키므로 this를 통해 생성한 프로퍼티와 메소드는 새로 생성된 객체에 추가된다.

3. 생성된 객체 반환

   - 반환문이 없는 경우, this에 바인딩된 새로 생성한 객체가 반환된다. 명시적으로 this를 반환하여도 결과는 같다.
     반환문이 this가 아닌 다른 객체를 명시적으로 반환하는 경우, this가 아닌 해당 객체가 반환된다. 이때 this를 반환하지 않은 함수는 생성자 함수로서의 역할을 수행하지 못한다. 따라서 생성자 함수는 반환문을 명시적으로 사용하지 않는다.

출처 : https://poiemaweb.com/js-this

```toc

```
