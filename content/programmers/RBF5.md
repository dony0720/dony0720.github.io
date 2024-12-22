---
emoji: 👨🏻‍💻
title: RBF 5회차 TypeScript interface와 type의 차이 - 1차 프로젝트 5팀
date: '2024-12-22 20:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 타입과 인터페이스의 차이점

타입스크립트에서 타입과 인터페이스는 모두 객체의 구조를 정의하는 데 사용되지만, 그 사용 목적과 기능에는 차이가 있다.

타입은 주로 변수, 함수 반환 값, 매개변수 등의 타입을 정의하는 데 사용된다.
인터페이스는 객체의 구조를 정의하고, 클래스가 특정 구조를 따르도록 강제하는 데 사용된다.
이 두 가지는 비슷해 보이지만, 실제로는 중요한 차이점이 있다.

왜냐하면 타입은 병합이 불가능하지만 인터페이스는 병합이 가능하기 때문이다.
이로 인해 인터페이스는 확장성과 재사용성이 높아진다.
타입스크립트 팀에서도 인터페이스 사용을 권장하고 있다.

## 타입과 인터페이스의 기본 선언

```ts
type User = {
  name: string;
  age: number;
};

interface User {
  name: string;
  age: number;
}
```

## 타입과 인터페이스 차이점

### (선언적 확장) 병합 가능 여부

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}

const user: User = {
  name: 'John',
  age: 30,
};
```

위의 예제에서 두 개의 인터페이스 선언이 병합되어 하나의 User 인터페이스가 생성된다.반면, 타입은 병합할 수 없다.

```ts
type User = {
  name: string;
};

type User = {
  age: number;
}; // 오류 발생
```

이로 인해 인터페이스는 확장성과 재사용성이 높아집 타입스크립트 팀에서도 인터페이스 사용을 권장하고 있다.
또한, 인터페이스는 클래스가 특정 구조를 따르도록 강제할 수 있다. 이는 코드의 일관성을 유지하는 데 도움이 된다. 반면, 타입은 이러한 기능을 제공하지 않는다.

### 확장(상속)

#### interface

extends 키워드를 이용해서 확장할 수 있다.

```ts
interface Person {
  name: string;
  age: number;
}

interface Student extends Person {
  // 확장(상속)
  school: string;
}

const student: Student = {
  name: 'Kim',
  age: 27,
  school: 'HY',
};
```

#### type

& 기호를 이용해서 확장할 수 있다.

```ts
type Person = {
  name: string;
  age: number;
};

type Student = Person & {
  // 확장(상속)
  school: string;
};

const student: Student = {
  name: 'Kim',
  age: 27,
  school: 'HY',
};
```

### 자료형

#### interface

**객체(Object)의 타입을 설정할 때 사용할 수 있으며, 원시 자료형에는 사용할 수 없다.**

```ts
interface Person {
  name: string;
  age: number;
  gender: string;
}
interface name extends string { // ❌ 불가능
  ...
}

```

#### type

객체 타입을 정의할 때도 사용할 수 있지만, 객체 타입을 정의할 때는 interface를 사용하는게 좋고,
단순한 원시값(Primitive Type)이나 튜플(Tuple), 유니언(Union) 타입을 선언할 때 type을 사용하는 것이 좋다.

```ts
type Name = string; // primitive
type Age = number;
type Person = [string, number, boolean]; // tuple
type NumberString = string | number; // union
type Person = {
  // 객체는 interface를 사용하도록 하자.
  name: string;
  age: number;
  gender: string;
};
```

### 유니온(|)과 교차(&)의 지원

```ts
// type: 유니온 타입 사용 가능
type Result = 'success' | 'error';

type UserInfo = {
  name: string;
  age: number;
} & {
  isAdmin: boolean;
};

// interface: 유니온 타입 직접 정의 불가 (별도 처리 필요)
interface UserInfo {
  // 단순 객체 정의에 사용
  name: string;
  age: number;
  isAdmin: boolean;
}
```

참고 ( 유니온과 교차에 대해 ): https://velog.io/@biosina1/TypeScript%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9C%A0%EB%8B%88%EC%96%B8%EA%B3%BC-%EA%B5%90%EC%B0%A8-%ED%83%80%EC%9E%85#%EA%B3%B5%ED%86%B5-%ED%95%84%EB%93%9C%EB%A5%BC-%EA%B0%96%EB%8A%94-%EC%9C%A0%EB%8B%88%EC%96%B8unions-with-common-fields

참고 : https://f-lab.kr/insight/typescript-type-vs-interface-20240801?gad_source=1&gclid=CjwKCAiA65m7BhAwEiwAAgu4JGUqcHv_3O-OmgxeLmBysvLCVk0HVyOpNUHplAQiqNnEA0e423sZnRoC1gcQAvD_BwE

참고: https://velog.io/@wlwl99/TypeScript-type%EA%B3%BC-interface%EC%9D%98-%EC%B0%A8%EC%9D%B4#%EC%9E%90%EB%A3%8C%ED%98%95type

```toc

```
