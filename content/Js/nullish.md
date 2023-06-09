---
emoji: 📝
title: Nullish 병합 연산자 (??) 
date: '2023-06-9 15:00:00'
author: Js 
tags: JS 
categories: Js  
---

# Nullish란
nullish 병합 연산자 (??) 는 왼쪽 피연산자가 `null` 또는 `undefined`일 때 오른쪽 피연산자를 반환하고,    
그렇지 않으면 왼쪽 피연산자를 반환하는 논리 연산자이다.

a ?? b의 평가 결과는 다음과 같습니다.

+ a가 null도 아니고 undefined도 아니면 a
+ 그 외의 경우는 b

nullish 병합 연산자 ??없이 x = a ?? b와 동일한 동작을 하는 코드를 작성하면 다음과 같습니다.

```
x = (a !== null && a !== undefined) ? a : b;
```

다른 예시를 보겠습니다!! 
```
let firstName = null;
let lastName = null;
let nickName = "바이올렛";

// null이나 undefined가 아닌 첫 번째 피연산자를 출력한다
console.log(firstName ?? lastName ?? nickName ?? "익명의 사용자"); // 바이올렛
``` 

지금은 firstName, lastName 이 `null` 이기 때문에 nickName을 반환합니다.    
하지만 nickName까지 null 또는 undefined면 "익명의 사용자"가 반환되겠죠? 

## "??"와 "||"의 차이 

```
let height = 0;

console.log(height || 100); // 100
console.log(height ?? 100); // 0 

```

### height || 100 결과
height에 0을 할당했지만 0을 falsy 한 값으로 취급했기 때문에 null이나 undefined를    
할당한 것과 동일하게 처리합니다. 따라서 height || 100의 평가 결과는 100입니다.

### height ?? 100 결과
height가 정확하게 null이나 undefined일 경우에만 100이 됩니다.    
예시에선 height에 0이라는 값을 할당했기 때문에 콘솔창에 0이 출력됩니다.

이런 특징 때문에 높이처럼 0이 할당될 수 있는 변수를 사용해서 기능을 개발할 땐    
||보다 ??가 적합합니다.

## 연산자 우선순위

??의 연산자 우선순위는 5로 꽤 낮습니다.

따라서 ??는 =와 ? 보다는 먼저, 대부분의 연산자보다는 나중에 평가됩니다.

그렇기 때문에 복잡한 표현식 안에서 ??를 사용해 값을 하나 선택할 땐    
괄호를 추가하는 게 좋습니다

```
let height = null;
let width = null;

// 괄호를 추가!
let area = (height ?? 100) * (width ?? 50);

alert(area); 
```

그렇지 않으면 *가 ??보다 우선순위가 높기 때문에 *가 먼저 실행 아래와 같게 됩니다.
```
let area = height ?? (100 * width) ?? 50;
``` 

## No chaining with AND or OR operators

AND (&&) 와 OR 연산자 (||)를 ??와 직접적으로 결합하여 사용하는 것은 불가능하다.    
이 경우 `SyntaxError`가 발생된다.

```
null || undefined ?? "foo"; // SyntaxError 발생
true || undefined ?? "foo"; // SyntaxError 발생
``` 

위와 같은 상황을 해결하고 위해서 우선 순위를 명시적으로 나타내 괄호를 사용하면 된다
```
(null || undefined ) ?? "foo"; // "foo" 반환 
```

참고 : <https://ko.javascript.info/nullish-coalescing-operator>   
참고 : <https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing>