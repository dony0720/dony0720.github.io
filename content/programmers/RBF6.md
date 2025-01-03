---
emoji: 👨🏻‍💻
title: RBF 1회차 유틸리티 타입 - 2차 프로젝트 4팀
date: '2025-01-03 22:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 유틸리티 타입 ( Utility Types )

TypeScript에서 제공하는 유틸리티 타입(Utility Types)은 기존 타입을 변형하거나 새로운 타입을 생성하기 위해 제공되는 내장 타입이다.
이를 사용하면 유틸리티 타입의 기능에 따라 타입 정의를 간결하고 유연하게 활용 할 수 있다.

## Partial<T>

모든 속성 값이 선택적(optional)으로 변경됨 객체의 일부 속성만 필요 할 때 활용된다.

```ts
type User1 = {
  name: string;
  age: number;
  address: string;
};

type PartialUser = Partial<User1>;

const user1: PartialUser = {
  name: 'Hong',
  // age나 주소가 옵셔널하게 변경됨
};
```

## Required<T>

모든 속성 값이 필수(Required)로 변경됨 객체의 모든 속성이 필요 할 때 활용된다.

```ts
type User2 = {
  name?: string;
  age?: number;
  address?: string;
};

type RequiredUser = Required<User2>;

const user2: RequiredUser = {
  name: 'hong',
  age: 12,
  address: '강남구',
};
```

## Readonly<T>

모든 속성 값을 읽기 전용(readonly)으로 변경함, 객체가 immutable 속성으로 변경된다.

```ts
type User3 = {
  name: string;
  age: number;
  address: string;
};

type ReadonlyUser = Readonly<User3>;

const readOnlyUser: ReadonlyUser = {
  name: 'Hong',
  age: 31,
  address: '서울시 강남구',
};

readOnlyUser.name = 'kim'; // 에러 발생! => 값의 변경을 허용하지 않음
```

## Pick<T, K>

타입에서 특정 속성만 선택(Pick)하여 새로운 객체 타입을 생성한다.

```ts
type User4 = {
  name: string;
  age: number;
  address: string;
};

type PickUser = Pick<User4, 'name' | 'address'>;

const user4: PickUser = {
  name: 'Hong',
  address: '서울시 강남구',
};
```

## Omit<T, K>

타입에서 특정 속성값을 제외(Omit)하여 새로운 객체 타입을 생성한다.

```ts
type User5 = {
  name: string;
  age: number;
  address: string;
};

type OmitUser = Omit<User5, 'name' | 'address'>;

const omitUser: OmitUser = {
  age: 31, // age만 필요!
};
```

## Record<K, T>

특정 키 집합(K)에 대해 값(T)의 모든 타입을 설정, 객체 타입을 생성할 때 활용한다.

```ts
type Roles = 'admin' | 'editor' | 'viewer';

type UserPermissions = Record<Roles, boolean>;

const permissions: UserPermissions = {
  admin: true,
  editor: false,
  viewer: true,
};
```

## NonNullable<T>

타입에서 null과 undefined를 제거, 값이 반드시 존재할 때 활용

```ts
type NullableType = string | null | undefined;

type NonNullableType = NonNullable<NullableType>;

const nonNullableValue1: NonNullableType = 'test';
// const nonNullableValue2: NonNullableType = null; // 에러!!
```

## Parameters<T>

함수 타입 T의 매개변수(parameter)들의 타입을 튜플(tuple)로 반환

```ts
function myFunc1(a: number, b: string): boolean {
  return true;
}

type Params = Parameters<typeof myFunc1>;

const params: Params = [42, 'hello'];
```

## ReturnType<T>

함수 타입 T의 반환값(return value) 타입을 추출한다.

```ts
function myFunc2(a: number): string {
  return '' + a;
}
type Returns = ReturnType<typeof myFunc2>;

const returnValue: Returns = 'test';
```

- type Returns에는 myFunc2의 반환값 string 타입을 추출하고 returnValue에 string 타입을 선언해준다.

```toc

```
