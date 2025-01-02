---
emoji: 👨🏻‍💻
title: Day 26 타입 단언, 타입 가드
date: '2025-01-02 22:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 타입 단언(Type Assertion) = as

1. Type 단언은 Type 추론을 활용하지 않고 특정 값이 특정 타입임을 강제로 지정하는 방법이다.
2. 컴파일러의 타입 추론 결과가 무시하고, 개발자가 원하는 타입을 지정 하는 방식이다.
3. 단, 타입 단언은 컴파일 단계에서만 작동하고 런타임 환경에서는 영향을 미치지 않는다.
4. 즉, 잘못된 Type 단언을 통해 런타임 에러가 발생할 수도 있으니 사용에 주의 필요하다!

## 기본 문법

```ts
let value1: any = 'Hello Typescript world!';
let value2: any = [1, 2, 3, 4, 5];
let length1: number = (value1 as string).length; //23
let length2: number = (value2 as number[]).length; // 5
```

## 빈 객체를 User Type으로 단언하는 문법

```ts
interface User {
  name: string;
  age: number;
}

const user1 = {} as User; // type 단언으로 빈객체 초기화
user1.name = 'Tom';
user1.age = 25;
```

# 타입 가드(Type Guard)

1. 런타임 시점에 특정 변수의 타입을 좁히거나 확정하기 위해 사용되는 기법이다.
2. 주로 Type에 대한 안정성을 확보하기 위해 활용 된다.
3. type은 기본형 외의 객체의 Type인 interface, alias, class를 포함한다.
4. typeOf, instanceOf, in, is 등의 연산자를 통해 타입 가드를 활용 할 수 있다.
5. Type에 대한 안정성을 확보하기 위한 문법으로 특정 변수의 Type을 보장 받지 못한 경우에만 활용된다.

## typeOf를 활용한 타입 가드

- 원시 타입(primitive type)을 확인하는 방법
- 특정 조건 내에서 변수의 타입을 좁혀(Type Narrowing) 타입을 추정하는 방법이다.

```ts
function printValue(value: unknown) {
  if (typeof value === 'string') {
    console.log(value.toUpperCase());
  } else if (typeof value === 'number') {
    console.log(value.toFixed(0));
  } else {
    console.log(value);
  }
}

printValue('abc'); // ABC
printValue(123.456); // 123
printValue(true); // true
```

## instanceof를 활용한 타입 가드

- 런타임에 객체가 특정 클래스의 인스턴스인지 확인하는 구문
- Javascript의 활용과 같다.

```ts
class Dog {
  sayDog(): void {
    console.log('왕왕!');
  }
}
class Cat {
  sayCat(): void {
    console.log('미야옹~');
  }
}

function sayAnimal(animal: Dog | Cat): void {
  if (animal instanceof Dog) {
    animal.sayDog();
  } else {
    animal.sayCat();
  }
}

sayAnimal(new Dog());
sayAnimal(new Cat());
```

## in을 활용한 타입가드

- 인터페이스와 type alias를 사용한 객체 타입을 구별 할 수 있는 방법
- 속성값을 기준으로 구별한다.
- (단, 같은 구성의 type은 구조적 타이핑으로 인해 타입이 호환됨으로 같은 type으로 취급한다.)

```ts
interface Student {
  name: string;
  grade: string; // "A", "B", "C"...
}

interface Employee {
  name: string;
  salary: number; // 8000000, 7000000 ....
}

const people1: Student = { name: 'Hong', grade: 'A' };
const people2: Employee = { name: 'Lee', salary: 4000000 };

function printPeople(p: Student | Employee): void {
  if ('grade' in p) {
    // 학생으로 추론
    console.log(p.name, 'Student', p.grade);
  } else {
    // 직장인으로 추론
    console.log(p.name, 'Employee', p.salary);
  }
}
```

## 사용자 정의 타입 가드 함수 (is 활용)

- is 키워드를 통해 사용자 정의 타입 가드를 구현 가능
- 이는 조건문 내에서 값의 타입을 좁혀주어, 해당 값이 특정 타입인지 확인할 수 있다.

```ts
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

console.log(isString('abc')); // true
console.log(isString(10)); // false

function print(value: unknown) {
  if (isString(value)) {
    console.log(value.toUpperCase()); // 타입이 string으로 좁혀짐
  } else {
    console.log('Not string');
  }
}

// 객체일 경우

type Member = { name: string; age: number };

function isMember(value: any): value is Member {
  return value && typeof value.name === 'string' && typeof value.age === 'number';
}

const m1: Member = { name: 'Hong', age: 21 };
const m2 = { name: 'Hong' };

console.log(isMember(m1)); // true
console.log(isMember(m2)); // false
```

```toc

```
