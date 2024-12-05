---
emoji: 👨🏻‍💻
title: Day 14 에러처리, 모듈화
date: '2024-12-05 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# Error

## Error 종류

1. SyntaxError 문법적으로 잘못된 코드를 실행하려고 할 때 발생

```
console.log('Hello); // 문자열 안 닫힘
```

2. ReferenceError 존재하지 않는 변수나 함수에 접근하려고 할 때 발생

```
console.log(x); // x is not defined
```

3. TypeError 변수나 값이 예상된 데이터 타입이 아닐 때 발생

```
null.foo(); // Cannot read properties
```

## try-catch 문

try: 에러 발생 가능한 코드를 작성
error: 에러 발생시 error문에 작성된 코드 실행
finally: 옵션 문장으로 에러 발생과 상관 없이 코드 실행

```js
try {
  if (true) {
    console.log('정상 영역');
  }
  let x = refValue;
} catch (error) {
  console.log('name : ', error);
  console.log('message : ', error.message);
} finally {
  // 항상 실행되는 문장
  console.log('call finally block!');
}
console.log('정상적인 영역3');
```

### 동작 원리

1. try 블록 실행

- console.log("정상 영역");가 실행된다
- let x = refValue;에서 refValue가 정의되지 않았으므로 **ReferenceError** 발생한다.

2. catch 블록 실행:

- 발생한 ReferenceError가 catch (error)로 전달됩니다.
- 에러의 이름(name)과 메시지(message)가 출력됩니다.
- error: 에러의 이름, error.message: 에러에 대한 자세한 내용

3. finally 블록 실행:

- 에러 발생 여부와 관계없이 항상 실행되는 블록이므로 "call finally block!"이 출력됩니다.

4. try-catch-finally 이후 코드 실행:

- console.log("정상적인 영역3")가 실행됩니다.
- 프로그램은 중단되지 않고 남은 코드를 계속 실행합니다.

# Module

## 모듈화의 필요성

1. 코드의 복잡도를 줄이기 위함이다.
2. 함수를 조각처럼 만들어서 쉬운 유지보수를 하기 위함이다. 함수에 에러 발생시 해당 함수만 수정되면 유지보수가 쉽다.
3. 만약 함수가 독립적인 아닌 의존적으로 연결되어 있다면 1개의 함수에 에러가 발생하게 되면 코드 전체를 수정해야하는 난관이 발생하기 때문이다.

## export와 import

- export: 작성된 함수를 외부파일로 내보낼때 사용된다.
- import: 외부에 작성된 함수를 가져올때 사용된다. head태그 내에서 작성한다.

외부에서 작성된 sayHello.js

```js
function sayHello(name) {
  return `Hello, ${name}`;
}

export default sayHello;
```

app.js

```js
import sayHello from './sayHello.js';

console.log(sayHello('Lee')); // Hello, Lee 출력
console.log(sayBye('Kim')); // Hello, Kim 출력
```

import는 확장자가 js인 파일에서 외부 함수를 가져올때 사용된다.

```toc

```
