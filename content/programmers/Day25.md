---
emoji: 👨🏻‍💻
title: Day 25 TypeScript
date: '2024-12-20 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# TypeScript

타입스크립트는 자바스크립트에 타입을 추가한 언어다. 타입을 검사하는 정적 타입 검사기이면서, 타입스크립트의 컴파일의 결과가 자바스크립트로 컴파일되는 언어이기도 하다. 확장자로는 .ts를 사용한다.

## TypeScript의 기본 타입

### 상속

자바스크립트의 기본 자료형들을 상속을 받아 활용한다.

```ts
let str: string = 'abc'; // type 지정은 소문자로!!
let num: number = 50;
let bool: boolean = true;
let undefined1: undefined = undefined;
let bigint1: bigint = 123456789123456789123456789123456789n;
let symbol: symbol = Symbol('key');

str = 1245; // str에 상속된 type이 달라 안된다!
num = 'test'; // num에 상속된 type이 달라 안된다!
```

### 참조

1. TS 참조형은 객체, 배열, 함수형으로 JS에서 활용하던 Type을 상속하여 추가적인 문법을 제공한다.
2. any은 어떤 type도 허용하는 타입으로 지정할수 있다. (사실상 javascript 변수)

```ts
let obj1 = { name: 'hong', age: 31 }; // 값 할당과 동시에 할당된 값의 type으로 정해진 상태
let arr1: Array<string> = ['a', 'b', 'c']; // 제네릭으로 생성
let arr2: number[]; // 배열 문법
arr2 = [1, 2, 3];
let tuple2: [number, number, boolean] = [1234, 5678, true];
let any1: Array<any></any> = [123, '문자열'];

obj1.name = 12; // 지정된 type과 달라 선언 불가!
```

- obj1은 각 프로퍼티에 값이 할당될때 할당된 값의 type으로 정해진다.
- arr1은 배열로 선언하고 인덱스의 값들은 string으로 받는다고 정의되어 있다. 제네릭으로 생성한다고 말한다.
- arr2은 배열로 정의하고 인덱스의 값들은 number로 받는다고 정의되어 있다.
- 튜플(tuple)은 배열의 일종으로 길이와 각 요소의 타입이 고정된 Type이다.
- any는 타입을 따지지 않는다.

## 배열

1. 배열의 선언법은 2가지로 대괄호( type [ ] ) 사용과 제네릭( Array < type > ) 사용 문법이 존재
2. 선언된 type만 배열 내에 삽입이 가능하며, any의 경우 모든 type의 변수를 허용한다.

```ts
let array1: Array<string> = ['a', 'b', 'c']; // 제네릭 문법
let array2: Array<any> = ['a', 12345, true];
let array3: number[] = [1, 2, 3, 4];
let array4: any[] = ['a', 12345, true];
let array5: object[] = [{ a: 10 }, { b: 20 }, { c: 40, d: 50 }];

let array6: number[][] = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];

let array7: Array<Array<number>> = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];
```

## 튜플(Tuple)

1. 튜플은 배열의 일종으로 길이와 각 요소의 타입이 고정된 Type이다.
2. 튜플은 any와 옵셔널(?) 연산이 존재하며, 옵셔널의 경우 값이 없어도 에러가 발생하지 않는다.

```ts
let tuple1: [string, number] = ['test', 1423];
let tuple2: [number, number, boolean] = [123, 456, true];
let tuple3: [any, any, any] = ['abc', 1234, true];
let tuple4: [string, string, string?] = ['abc', 'def', 'ehg']; // 옵셔널 적용!
let tuple5: [string, string?, string?] = ['abc', 'def']; // 옵셔널 적용!
let tuple6: [string, string?, string?] = [...tuple6]; // 스프레드 연산자 활용!
```

## Type 추론

TypeScript는 정적 타입 시스템을 통해 변수가 어떤 타입인지 미리 선언하거나 추론할 수 있다.

```ts
let str2 = 'abc'; // type추론에 의해 str2 문자열 type으로 지정됨
let number2 = 12345;
let bool2 = true;
let arr3 = [1, 2, 4, 4];
```

## TypeScript 함수

1. TypeScript에서 함수는 매개변수와 반환 값의 타입을 명시하여 선언이 가능하다.
2. 이때 매개 변수의 Type은 생략 불가능하며, 반환 값은 생략 가능하다.

```ts
// TS 함수 선언 (인자와 return type 추가)
function add(a: number, b: number): number {
  return a + b;
}
let result: number = add(3, 5);

// 리턴 type 생략은 가능, 인자는 불가!
function multi(a: number, b: number) {
  return a * b;
}
let result2: number = multi(3, 5);
```

```
function 함수명 (매개변수: type 지정): 반환값 type지정 {
    return 반환할 값
}
```

### void 키워드, 옵셔널 매개변수, rest(나머지 값) 매게 변수

void 키워드 : 함수의 **리턴 값이 없을 때** 명시적으로 붙일 수 있는 키워드

```ts
function printValue(str: string): void {
  // return "11"; error!
  console.log(str);
}
```

옵셔널 매개변수( ? ) : 매개변수의 값이 있어도 되고 없어도 되는 값으로 여겨진다.

```ts
// 옵셔널 인자 활용
function sayHello(name: string, age?: number): void {
  console.log(name, age || '나이 모름');
}

sayHello('Hong'); // Hong
sayHello('Hong', 25); // Hong 25
```

rest 매개변수

```js
// rest(=나머지 값) 매개변수
function sum(...numbers: number[]): number {
  return numbers.reduce((prev, cur) => prev + cur, 0);
}

let sumValue1 = sum(1, 2, 3);
```

- sum 에서 받아온 인수를 ...(스프레드)를 통해 하나의 배열로 묶는다
- 각 배열의 값을 합쳐 반환한다.

```toc

```
