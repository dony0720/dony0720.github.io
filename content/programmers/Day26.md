---
emoji: 👨🏻‍💻
title: Day 26 interface, union, type
date: '2024-12-23 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# interface

## 함수 interface 정의

1. 함수의 인자와 리턴 타입에 대한 인터페이스를 정의하여 함수의 형태를 지정할 수 있다.
2. 함수 interface는 함수 구조의 상속이나 callback 구조의 제한으로도 활용 할 수 있다.

```ts
interface calc {
  (a: number, b: number): number;
}

const add: calc = (x, y) => x + y;
const minus: calc = (x, y) => x - y;
const multi: calc = (x, y) => x * y;
const divide: calc = (x, y) => x / y;

// callback 함수 예제
function printLog(callback: calc, a: number, b: number) {
  console.log(callback(a, b));
}
printLog(add, 3, 5);
```

## 상속

1. 상속은 객체 타입을 확장하여 다른 인터페이스의 속성을 포함하거나 덮어쓰는 데 사용된다.
2. 인터페이스는 extends 키워드를 사용하여 상속이 가능하다.

```ts
interface Parent {
  name: string;
  age: number;
}

interface Child extends Parent {
  // name:string; // 상속 받은 값1
  // age:number; // 상속 받은 값2
  address?: string;
  mailing?: boolean;
}

const parent1: Parent = { name: 'Hong', age: 31 };

const child1: Child = {
  name: 'John',
  age: 25,
  address: '서울시 강남구',
  mailing: false,
};
```

### 속성 범위 축소

자식에서 부모의 type범위를 축소하는 것이 가능하다. ( 확장 불가 ❌)

```ts
interface Parent2 {
  id: string | number; // union
  age: number;
}

interface Child2 extends Parent2 {
  id: string; // id의 범위를 축소!
  name: string;
}

const parent2: Parent2 = { id: 10, age: 31 };
const parent3: Parent2 = { id: 'test', age: 31 };

const child5: Child2 = { id: 'test', age: 31, name: 'hong' };
```

### 다중 상속

인터페이스는 다중상속이 가능함으로 다중 확장을 지원

```ts
interface A {
  name: string;
}
interface B {
  age: number;
}
interface C {
  mailing: boolean;
}

interface Child3 extends A, B, C {
  address?: string; // 옵셔널 (있어도 되고 없어도 되는 값)
}

const child6: Child3 = { name: 'Hong', age: 15, mailing: false };

const child7: Child3 = {
  name: 'Hong',
  age: 15,
  mailing: false,
  address: '서울시 강남구',
};
```

## 배열 인덱싱 타입 정의

1. 인터페이스를 사용한 배열 인덱싱은 인덱스 시그니처를 통해 구현이 가능하다.
2. 배열이 특정 요소 타입을 가지도록 인터페이스를 정의하거나,
3. 배열을 객체로 간주하여 숫자 또는 문자열 기반 인덱스를 설정이 가능하다.

```ts
// index는 number, 값은 문자열 type
interface StringArray {
  [index: number]: string; // index - 시그니처
}

let array1: StringArray = ['str1', 'str2', 'str3'];
// let array2: StringArray = ["str1", "str2", 123];
// number 타입이 값에 들어가면 에러를 발생 (number 타입을 지정해주지 않았기 때문이다.)

// index와 값이 모두 문자열
interface StringArray2 {
  [index: string]: string;
}
// => 에러 발생 index의 값이 문자열이 되면 배열을 생성할 수 없기때문이다.
```

## 객체 인덱싱 타입 정의

1. 배열 인덱싱을 기반으로 객체 인덱스도 정의 가능하다.
2. 이때 내부 타입을 다양하게도 선언이 가능하다.

```ts
interface StrToNumMap {
  [level: string]: number;
}

let object1: StrToNumMap = {
  초급: 3000000,
  중급: 5000000,
  고급: 7000000,
};

console.log(object1['고급']);

// index와 값이 string type인 interface
interface StrToStrMap {
  [key: string]: string;
}
let colors: StrToStrMap = {
  apple: '빨강',
  banana: '노랑',
  cherry: '빨강',
};
```

# Union

1. 하나 이상의 타입을 가질 수 있는 값을 정의하는 데 사용
2. 유니온 타입은 | (파이프) 기호를 사용하여 여러 타입을 결합 가능하다.

```ts
let numAndStr: number | string;
numAndStr = 'abc';
numAndStr = 100;
```

## 특정 문자열(리터럴)로 구성된 union 설계

```ts
let myAuthority: 'admin' | 'user' | 'vip';

myAuthority = 'admin';
myAuthority = 'user';

// myAuthority = null; // 허용 안됨!
// myAuthority = "member"; // 허용 안됨!
```

지정된 문자열 이외에는 허용되지 않는다.

# type

## 기본 타입의 type alias 사용

1. 기본 타입의 type alias는 alias 문법만 사용 가능하며, interface로는 표현이 불가능하다.
2. union 활용 : 기본형 union과 사용자 리터럴을 결합하여 다양한 type을 결합한 type 생성 가능
3. nullable 패턴 : 유니온 타입의 null을 포함하면 null을 허용하게 끔 설계 할 수 있다.

```ts
type UserId = number | string;
type Password = string;
type UserName = string | null;
type Authrity = 'USER' | 'ADMIN' | null;
type UnionType = UserId | UserName;

let id1: UserId = 'test1';
let name1: UserName = 'hong';
let name2: UserName = null;
let authrity1: Authrity = 'USER';
let authrity2: Authrity = null;
```

## 객체의 type alias 활용

type alias를 통해 객체의 별칭을 정할수 있다.

```ts
// type을 통한 User 객체 설계
type User = {
  name: string;
  age: number;
  mailing?: boolean;
  hobby?: string[];
};

let user1: User = { name: 'hong', age: 31, mailing: true, hobby: ['축구', '영화보기'] };
```

### 객체의 type alias 상속(&=Intersection)

상속과 같은 메커니즘도 활용 가능한데, type alias의 상속은 &(Intersection) 연산을 활용

```ts
type Parent1 = {
  name: string;
  age: number;
};

type Parent2 = {
  address: string;
  mailing?: boolean;
};

// 상속하는 방법1
type Child1 = Parent1 & Parent2;

// 상속하는 방법2
type Child2 = Parent1 & {
  address: string;
  mailing?: boolean;
};

// 선언
const parent1: Parent1 = {
  name: 'Hong',
  age: 31,
};

const child1: Child1 = {
  name: 'Hong',
  age: 31,
  address: '서울시 강남구',
  mailing: false,
};

const child2: Child2 = { ...parent1, address: '서울시 강남구', mailing: false };
const child3: Child2 = { ...child1 };
```

```toc

```
