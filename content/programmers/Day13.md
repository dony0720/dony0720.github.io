---
emoji: 👨🏻‍💻
title: Day 13 클래스, 배열
date: '2024-12-04 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# Class

## Class 선언식

```js
class Person {
  height = 170;
  // 생성자
  constructor(name, age) {
    this.name = name; // 속성 정의
    this.age = age;
  }
  // sayHello = function(){}

  // 메서드 정의, 자동으로 prototype에 지정됨
  sayHello() {
    console.log(`Hello, my name is ${this.name}, and I am ${this.age} years old.`);
  }
}

// 객체 생성
const person1 = new Person('Tom', 31);
const person2 = new Person('Kim', 24);
const person3 = new Person('Lee', 17);
```

- constructor는 생성된 인스턴스에 전달되는 인자 값이다.
- 클래스 내부에 정의된 메서드는 prototype에 추가되어 인스턴스간에 공용으로 사용가능하고 메모리를 효율적으로 사용할 수 있다.

## Class 표현식

```js
const Dog = class /*Dog2*/ {
  constructor(dogName) {
    this.dogName = dogName;
  }
  speak() {
    console.log(`${this.dogName} : 컁컁`);
  }
};
const dog = new Dog('토토');
dog.speak();
```

## getter & setter

- getter : 값을 가져오는 역할의 키워드로 메서드 이름 앞에 get을 붙인다.
- setter : 값을 할당하는 역할을 키워드로 메서드 이름 앞에 set을 붙인다. 단 setter에는 하나의 인자만 설정할 수 있다.

```js
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  get area() {
    // 면적 계산: 게터
    return this.width * this.height;
  }
  set setHeight(height) {
    // 높이 설정: 세터
    this.height = height;
  }
  get printStr() {
    // 출력 문장
    return `width : ${this.width}, ` + `height : ${this.height}, ` + `area : ${this.area}`;
  }
}
```

## static 키워드

```js
class StaticTest {
  constructor(instanceValue) {
    this.instanceValue = instanceValue;
  }
  static staticValue = 100;
  static staticMethod() {
    console.log('static value : ' + this.staticValue);
  }
}
let instance = new StaticTest('test');

// 생성된 인스턴스 값 호출
let instance = new StaticTest('test');
console.log(instance.instanceValue); // test
console.log(instance.staticValue); // undefined
// instance.staticMethod(); // error!

// static 키워드로 정의된 속성값, 메소드 호출ㄴ
console.log(StaticTest.instanceValue); // undefined
console.log(StaticTest.staticValue); // 100
StaticTest.staticMethod(); // static value : 100
```

static 키워드로 정의된 속성 또는 메서드가 있다면 외부에서 인스턴스의 생성없이 접근할 수 있다.

## Class의 호이스팅

Class는 호이스팅을 지원하지 않으며, Class가 선언 된 이후 라인에서 Class를 사용할 수 있다.

```js
class ClassA {}
class ClassB {}
const instance1 = new ClassA();
const instance2 = new ClassB();
const instance3 = new ClassC(); // 에러문장!!

class ClassC {}
```

## public과 private

- Public: 클래스 외부에서 자유롭게 접근 가능
- Private: 클래스 내부에서만 접근 가능

```js
class BankAccount {
  #balance = 0; // private field

  constructor(owner) {
    this.owner = owner; // public field
  }

  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
    }
  }

  getBalance() {
    return this.#balance; // private 데이터 접근
  }
}

const account = new BankAccount('John');
account.deposit(100);
console.log(account.getBalance()); // 100
console.log(account.#balance); // ❌ Error: Private field
```

private를 사용하는 이유는 외부에서 데이터를 무분별하게 수정하지 못하게 막아 불필요한 오류를 예방하기 하기 위함이다.

## Class 상속

### extends

```js
class Parent {
  constructor(pValue) {
    this.pValue = pValue;
  }
  greet() {
    console.log('Hello from Parent');
  }
}

class Child extends Parent {
  sayHello() {
    console.log('Hello from Child');
  }
}

let p1 = new Parent('test1');
let c1 = new Child('test');
p1.greet(); // Hello from Parent
c1.greet(); // Hello from Parent
c1.sayHello(); // Hello from Child
console.log(c1.pValue); // test
```

### super 키워드

super키워드는 부모의 생성자를 호출하거나 메서드를 호출하기 위한 방법으로 활용

```js
// 부모
class Parent2 {
  constructor(pValue) {
    this.pValue = pValue + 1;
  }
  greet() {
    console.log('Hello from Parent');
  }
}

// 자식
class Child2 extends Parent2 {
  constructor(pValue, cValue) {
    super(pValue); // Parent2에 정의된 생성자 호출. 즉, this.pValue = pValue + 1로 할당된다.
    this.cValue = cValue;
  }

  sayHello() {
    super.greet(); // 부모의 greet
    console.log('Hello from Child');
  }

  getParentValue() {
    return this.pValue; // 부모의 속성은 this로 접근필요!! super 불가
  }
}
let p2 = new Parent2('test1');
const c2 = new Child2('pTest', 'cTest');
console.log(c2); // Child2 { pValue: 'pTest1', cValue: 'cTest' }
c2.sayHello(); // Hello from Parent // Hello from Child
console.log(c2.getParentValue()); // pTest1
```

super 키워드

1. 생성자 (constructor)에 적용시 부모(Parent2)에 정의된 생성자 함수로 값을 정의하게 된다. 즉, this.pValue = pValue + 1로 할당된다.
2. 메서드에 키워드 적용시 부모(Parent2)에 정의된 메서드를 호출한다.
3. return 에는 super 키워드가 적용되지 생성자에서 부모의 값을 할당받아야 한다.

## Class 재정의

```js
// 메서드 재정의
class Parent3 {
  sayHello() {
    console.log('Hello from Parent!');
  }
}

class Child3 extends Parent3 {
  // 재정의하는 법 = 메소드 선언과 같음
  sayHello() {
    console.log('Hello from Child!!!');
  }
}

const c3 = new Child3();
c3.sayHello(); // Hello from Child!
console.log('----------------------------------------------------------');

// 속성 재정의
class Parent4 {
  constructor() {
    this.a = 10;
    this.b = 20;
  }
}
class Child4 extends Parent4 {
  constructor() {
    super();
    this.a = 100;
    this.b = 200;
  }
}
const parent4 = new Parent4();
const child4 = new Child4();
console.log(parent4); // Parent4 { a: 10, b: 20 }
console.log(child4); // Child4 { a: 100, b: 200 }
```

# Array

## 배열 결합시 많이하는 실수

```js
var array1 = ['사과', '바나나', '키위'];
var array2 = ['키위', '수박', '파인애플'];
var array6 = [array1, array2]; // [ [ '사과', '바나나', '키위' ], [ '키위', '수박', '파인애플' ] ]
var array7 = array1 + array2; // 출력값: 사과,바나나,키위키위,수박,파인애플
```

- array6는 각 배열을 하나의 인덱스 값으로 정의하기 때문에 위와 같은 결과값이 나온다
- 각 배열을 + 연산자를 사용하면 문자열로 합쳐진다

## reduce()

배열의 각 요소를 단일 값으로 축소하는 메서드이다.

### sum 예제

```js
var array = [1, 2, 3, 4, 5];

var sum = array.reduce((prev, cur) => {
  console.log(prev, cur);
  return prev + cur;
}, 0); // 초기값 0
console.log(sum);
```

- prev : 기존 계산 값, cur : 현재 값, initialValue: 초기값
  1. prev에는 초기값 0, cur에는 array배열의 처음값인 1이 들어간다.
  2. 배열 길이만큼 순회문을 돌면서 prev에는 기존 계산 값, cur에는 배열의 값을 가져온다
  3. 순회문을 돌면 다음과 같이 출력된다. (0,1), (1,2), (3,3), (6,4), (10,5)
  4. sum에는 마지막 순회문의 결과값인 15가 저장된다.

### 개수 세기

```js
const fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple'];
const fruitCounts = fruits.reduce((counter, fruit) => {
  if (fruit in counter) {
    counter[fruit]++; // key의 value 값 증가
  } else {
    counter[fruit] = 1; // key-value 설정
  }
  return counter;
}, {});
console.log(fruitCounts); // { apple: 3, banana: 2, orange: 1 }
```

- counter: 초기값 할당, fruit: 각 배열의 값 할당, {}: counter의 초기값 설정
  1. counter 객체에 fruits 배열에서 해당 과일이 있으면 counter 객체에서 해당 과일의 key를 찾고 value를 1 증가 시킨다.
  2. 만약에 사과가 없다면 else 문으로 이동해 counter["apple"] = 1에 의해 counter 객체에 apple : 1 이 저장된다.
  3. 반복문이 종료되면 counter 객체를 반환시킨다.

## sort()

### 문자열 정렬

```js
var arr2 = [
  '홍길동',
  '박길동',
  '김동길',
  '차길동',
  '김길동',
  '홍동길',
  '최길동',
  '팍길동',
  '이길동',
];
console.log('기본(오름차순) : ' + arr2.sort());
console.log('내림차순 : ' + arr2.sort().reverse());
console.log('내림차순(람다함수) : ' + arr2.sort((x, y) => y.localeCompare(x)));
console.log('내림차순(람다함수) : ' + arr2.sort((x, y) => x.localeCompare(y)));
```

### 숫자 정렬

```js
var arr1 = [10, 492, 20, 3212, 12, 322, 4, 262, 800];

console.log('오름차순 정렬(람다) : ' + arr1.sort((x, y) => x - y));
console.log('내림차순 정렬(람다) : ' + arr1.sort((x, y) => y - x));
```

문자열 정렬에는 sort()만으로 정렬이 되지만 숫자 정렬에는 적용되지 않아 위와 같이 작성해 주어야 한다.

```toc

```
