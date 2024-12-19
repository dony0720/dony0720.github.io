---
emoji: 👨🏻‍💻
title: WTL 4회차 this 바인딩 - 1차 프로젝트 5팀
date: '2024-12-12 22:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# this란

**this**는 JavaScript에서 객체의 문맥(context) 또는 호출 환경을 참조하는 키워드로, 특정 함수나 코드 블록이 실행되는 동안의 현재 객체를 나타낸다.

## 함수 호출 방식에 의해 결정되는 this

javaScript에서는 호출 방식에 의해 this에 바인딩할 객체가 동적으로 결정된다.
바인딩: 변수, 함수, 또는 this와 같은 식별자가 특정 값이나 객체에 연결되는 과정을 의미한다.

## 함수 호출에서의 this

### 전역에서 함수 선언

전역에서의 모든 함수의 this는 window 객체를 바인딩한다.

```js
var ga = 'Global variable';

console.log(ga);
console.log(window.ga);

function foo() {
  console.log('invoked!');
}
window.foo();
```

### 내부함수

함수의 내부 함수에서 this 또한 window 객체를 바인딩한다.

```js
function foo() {
  console.log("foo's this: ", this); // window
  function bar() {
    console.log("bar's this: ", this); // window
  }
  bar();
}
foo();
```

### 객체의 메서드, 메서드의 내부함수, 콜백 함수

- 객체에서의 메서드일 경우에는 this에 해당 객체가 바인딩된다.
- 단, 메서드의 내부함수일 경우에는 window 객체를 바인딩한다.
- setTimeout 같은 콜백함수에서의 this도 window 객체를 바인딩한다.

```js
var value = 1;

var obj = {
  value: 100,
  foo: function () {
    console.log("foo's this: ", this); // obj
    console.log("foo's this.value: ", this.value); // 100
    function bar() {
      console.log("bar's this: ", this); // window
      console.log("bar's this.value: ", this.value); // 1
    }
    setTimeout(function () {
      console.log("callback's this: ", this); // window
      console.log("callback's this.value: ", this.value); // 1
    }, 100);
    bar();
  },
};

obj.foo();
```

## 생성자 함수애서의 this

new 키워드로 호출된 생성자 함수에서는 this가 새로 생성된 객체를 참조한다.

```js
// 생성자 함수
function Person(name) {
  this.name = name;
}

var me = new Person('Lee');
console.log(me); // Person&nbsp;{name: "Lee"}
```

## 명시적 this 바인딩

### call

- call() 메서드는 첫 번째 인자에 this를 설정하고, 나머지 인수를 개별적으로 전달한다고 한다.
- greet 함수에서 this는 person을 참조한다.
- greeting = 'Hello', punctuation='!' 가 할당된다.

```js
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: 'Alice' };

greet.call(person, 'Hello', '!'); // "Hello, Alice!"
```

### apply

apply는 call 메서드와 거의 동일하지만 인자를 배열로 전달한다는 차이가 있다.

```js
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: 'Alice' };

greet.apply(person, ['Hi', '.']); // "Hi, Alice."
```

### bind

bind() 메서드는 함수를 호출하지 않고, this가 고정된 새로운 함수를 반환합니다. 이후 반환된 함수를 호출하면 this는 항상 설정된 값을 참조합니다.

```js
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: 'Alice' };

const boundGreet = greet.bind(person, 'Hey');
boundGreet('!'); // "Hey, Alice!"
```

- 아래 코드는 bind 함수를 apply의 관점으로 자세하게 분석한 코드이다.

```js
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: 'Alice' };

// `bind()`를 사용한 것과 동일한 동작을 수행하는 함수
const boundGreet = function (...args) {
  // `apply`를 사용해 this를 고정
  return greet.apply(person, args); // `person`으로 this 고정, `args`는 전달된 인수 배열
};

// 호출
boundGreet('Hey', '!'); // "Hey, Alice!"
```

1. boundGreet는 익명 함수로 정의된다다.
2. 이 익명 함수는 호출될 때 greet.apply(person, args)를 실행한다.
   - 여기서 person이 this로 고정됩니다.
   - args는 호출 시 전달된 모든 인수(greeting, punctuation)를 포함합니다.
3. apply는 greet 함수에 person과 전달된 인수를 적용하여 호출합니다.

### arrow function

arrow function은 this 바인딩할 객체가 선언할 때 정적으로 결정된다. **즉, 언제나 상위 스코프의 this를 가르킨다 이를 Lexical this 라한다.**

```js
const obj = {
  name: 'Alice',
  greet: function () {
    const arrowFunc = () => {
      console.log(this.name); // this => obj
    };
    arrowFunc();
  },
};

obj.greet(); // "Alice"
```

```toc

```
