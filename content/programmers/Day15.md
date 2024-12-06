---
emoji: 👨🏻‍💻
title: Day 15 구조 분해 할당, 전개구문(...), async & await
date: '2024-12-06 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 구조 분해 할당

객체 또는 배열의 값을 선언된 변수의 순서에 따라 값을 할당한다.

```js
// 기본적인 구조 분해 할당
const array = [1, 2, 3];
const [a, b, c] = array;

// 값을 할당할 변수가 모자를 경우
let person = { name: 'Bob', age: 30, address: '서울시 강남구' };
const { name, age } = person; // address는 구조분해할당 제외!!
console.log(name, age); // name: Bob, age: 30 출력
```

# 전개구문 (...)

- 전개구문 ... 을 사용하게 되면 배열의 전체 또는 일부를 복사할 수 있다. (본래의 값은 변하지 않는다.)

## 전개 구문 활용

### 배열 내용 조합

```js
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const arr3 = [7, 8, 9];
const arrWrap = [...arr1, ...arr2, ...arr3];

console.log(arrWrap); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```js
const arr = [4, 5, 6];
const arrWrap = [1, 2, 3, ...arr, 7, 8, 9];

console.log(arrWrap); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

배열의 전개 구문은 위와 같이 아무데서 사용이 가능하다고 한다

### 배열 복사하기

```js
const myArray1 = ['a', 'b', 'c', 'd', 'e'];
console.log(...myArray1); // 'a', 'b', 'c', 'd', 'e'
const myArray2 = [...myArray1]; // ...myArray1 : 'a', 'b', 'c', 'd', 'e'

console.log(myArray1); // ["a", "b", "c", "d", "e"]
console.log(myArray2); // ["a", "b", "c", "d", "e"]

console.log(myArray1 === myArray2); // false
```

myArray2는 myArray1 을 전개구문을 통해 복사했지만 둘은 엄연히 독립적이기 때문에 다른 값이다

### 배열의 비구조화 할당

```js
const [first, second, ...rest] = [1, 2, 3, 4, 5];

console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3, 4, 5]
```

### 배열의 나머지 요소 할당

```js
const [first, second, ...rest] = [1, 2, 3, 4, 5];

console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3, 4, 5]
```

- 변수 first과 second의 각각의 인덱스 값에 맞는 값이 차례로 들어가고(1, 2), rest에는 할당 받지 못한 나머지 값들이 **하나의 배열로 묶여 대입된다.**
- 🚨주의점🚨 : 다음 선언문과 같이 나머지 전개구문이 마지막 요소에 선언하지 않으면 구조 파괴로 선언될 수 없다. `const [first, ...rest, second] = [1, 2, 3, 4, 5]`

### 전개구문으로 파라미터를 받는 경우 => 리턴값 : 배열

```js
function sumAll(...args) {
  // args는 배열입니다.
  let sum = 0;

  for (let arg of args) sum += arg;

  return sum;
}

console.log(sumAll(1)); // 1
console.log(sumAll(1, 2)); // 3
console.log(sumAll(1, 2, 3)); // 6
```

1. 전개연사자를 사용해 인수 리스트를 배열로 하나로 묶어서 받는다. 예를 들어 args = 1,2,3의 값으로 독립적으로 있다면 전개구문을 통해서 ...args = [1,2,3]이 되는것이다.
2. 하나의 배열로 묶은 args를 for 반목문을 통해 배열의 각 요소를 sum에 더한 후에 값을 반환한다.

```js
function showName(firstName, lastName, ...titles) {
  alert(firstName + ' ' + lastName); // Julius Caesar

  // 나머지 인수들은 배열 titles에 할당됩니다.
  // titles = ["Consul", "Imperator"]
  alert(titles[0]); // Consul
  alert(titles[1]); // Imperator
  alert(titles.length); // 2
}

showName('Julius', 'Caesar', 'Consul', 'Imperator');
```

1. firstName = "Julius" , lastName = "Caesar", titles = ["Consul","Imperator"] 를 할당한다.
2. titles는 전개구문으로 나머지 값으로 할당 받고 배열로 리턴하기 때문에 위와 같은 결과가 나온다.

## 왜 객체는 console.log(...object) 동작이 되지 않는가

### 전개구문의 동작원리

전개 구문은 **이터러블**한 데이터 구조를 펼치는데 사용한다.

- 이터러블: 배열, 문자열, Map, Set등 반복가능한 데이터 구조를 말한다.
- 객체는 key-value의 값으로 이루어져 있어 이터러블한 값이 아니라고 한다.

### 해결법

Object.entries나 Object.values를 사용해 객체를 배열로 변환 시켜주면 된다고 한다.

```js
const obj = { a: 1, b: 2, c: 3 };

console.log(...Object.values(obj)); // 1 2 3
console.log(...Object.entries(obj)); // ['a', 1] ['b', 2] ['c', 3] key-value를 배열로 반환 시킨다.
```

### 응용

```js
const obj = { a: 1, b: 2, c: 3 };
for (const [key, value] of Object.entries(obj)) {
  console.log(key, value);
}
// 출력:
// a 1
// b 2
// c 3
```

# async & await

비동기 함수를 동기 함수로 바꿔주는 역할을 한다.

- 동기 : 1번 작업이 마무리 되면 2번작업을 진행하는 것과 같은 직렬 방식이라고 생각하면된다.
- 비동기 : 1번 ,2번 작업이 동시에 시작되는 병렬 방식이라고 생각하면된다.
- Promise : 비동기 함수의 결과를 담고 있는 객체이다.
- async : async 키워드는 함수 앞에 붙여서 해당 함수를 비동기 함수로 선언한다. 함수를 호출할때 직렬이 아닌 병렬로 함수들이 동작될 수 있게 하기 위함이다.
- await : Promise가 해결될 때까지 기다렸다가 결과값을 반환한다. 즉, 함수 내부에서는 직렬 방식으로 진행될 수 있게 만들어준다.

```js
async function fetchData() {
  // 비동기 처리를 위해선 보통 try-catch문을 감싸서 해결한다.
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.log('error: ' + error);
  }
}
```

동기 함수 동작 원리

1. response 변수에는 해당 url의 정보를 가져올때까지 다음 줄의 코드를 동작시키지 않는다.
2. response에 값이 할당되면 data 변수에서 response의 값을 json 형태로 변환시킨다.
3. 변환 시킨 후에는 콘솔창에 json 형태로 바뀐 data를 출력하게 한다.

```toc

```
