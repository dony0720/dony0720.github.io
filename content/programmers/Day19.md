---
emoji: 👨🏻‍💻
title: Day 19 javaScript 과제 정리
date: '2024-12-12 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# Practice_03

## 문제 3

- 입력 받은 정수가 양수이면서 짝수일 때만 “짝수다”를 출력하고
- 짝수가 아니면 “홀수다“를 출력하세요.
- 양수가 아니면 “양수만 입력해주세요.”를 출력하세요.

### solution

```js
// 내가 적은 답안
function practice4(num) {
  if (num > 0) {
    if (num % 2 === 0) {
      console.log('짝수입니다');
    } else {
      console.log('홀수입니다');
    }
  } else {
    console.log('양수만 입력해주세요');
  }
}

// 다른 답안

function practice4(num) {
  if (!num || isNaN(num) || num < 0 || !Number.isInteger(num)) {
    console.log('양수만 입력하세요.', num);
    return;
  }

  if (num % 2 == 0) {
    console.log('짝수다');
  } else {
    console.log('홀수다');
  }
}
```

## 문제 7

- 실습문제7
- 아이디, 비밀번호를 test/1212로 정하고 로그인 기능을 작성하세요.
- 로그인 성공 시 “로그인 성공”,
- 아이디가 틀렸을 시 “아이디가 틀렸습니다.“,
- 비밀번호가 틀렸을 시 “비밀번호가 틀렸습니다.”를 출력하세요.

### solution

```js
// 내 답안
function practice7(id, pw) {
  if (id === 'test') {
    if (pw === 1212) {
      console.log('로그인 성공 ');
    } else {
      console.log(' 비밀번호가 틀렸습니다');
    }
  } else {
    console.log('아이디가 틀렸습니다');
  }
}

// 다른 답안
function practice7(id, password) {
  const userId = 'test';
  const userPw = '1212';

  if (!id || !password) {
    console.log('잘못된 입력입니다.');
    return;
  }
  if (userId != id) {
    console.log('아이디가 틀렸습니다.');
    return;
  }
  if (userPw != password) {
    console.log('비밀번호가 틀렸습니다.');
    return;
  }
  // 여기가 정상 케이스
  console.log('로그인 성공!');
}
```

if문에서 return을 만나면 함수 실행을 종료한다는 점을 이용해 코드의 가독성을 높이는걸 볼 수 있었습니다.

## 문제 8

- 두 개의 정수와 연산 기호를 입력 받아 연산 기호에 맞춰 연산 결과를 출력하세요.
- 단, 두 개의 정수 모두 양수일 때만 작동하며 없는 연산 기호를 입력 했을 시 “잘못 입력하셨습니다. 프로그램을 종료합니다.” 출력

### solution

```js
// 내 솔루션
function practice8(num1, num2, operator) {
  if (num1 > 0 && num2 > 0) {
    switch (operator) {
      case '+':
        console.log(num1 + num2);
        break;
      case '-':
        console.log(num1 - num2);
        break;
      case '*':
        console.log(num1 * num2);
        break;
      case '/':
        console.log(num1 / num2);
        break;
      case '%':
        console.log(num1 % num2);
        break;
      case '**':
        console.log(num1 ** num2);
        break;
      default:
        console.log('잘못 입력하셨습니다. 프로그램을 종료합니다');
    }
  } else {
    console.log('모두 양수를 입력해 주세요');
  }
}

// 다른 답안

function practice8(x, y, operator) {
  if (
    !x ||
    !y ||
    !operator ||
    isNaN(x) ||
    isNaN(y) ||
    !Number.isInteger(x) ||
    !Number.isInteger(y) ||
    x < 1 ||
    y < 1
  ) {
    console.log('잘못 입력하셨습니다. 프로그램을 종료합니다.', arguments);
    return;
  }

  let result;
  switch (operator) {
    case '+':
      result = x + y;
      break;
    case '-':
      result = x - y;
      break;
    case '*':
      result = x * y;
      break;
    case '/':
      result = x / y;
      break;
    case '%':
      result = x % y;
      break;
    case '**':
      result = x ** y;
      break;
  }

  if (result == null) {
    console.log('잘못 입력하셨습니다. 프로그램을 종료합니다.', arguments);
    return;
  }

  // 여기가 정상 케이스
  console.log('피연산자1 입력값 :', x);
  console.log('피연산자2 입력값 :', y);
  console.log('연산자를 입력 값(+,-,*,/,%,**) :', operator);
  console.log(`${x} ${operator} ${y} = ${result}`);
}
```

# Practice_04

## 문제4

- 두 개의 값을 입력 받아 그 사이의 숫자를 모두 출력하세요.
- 만일 1 미만의 숫자가 입력됐다면 “1 이상의 숫자를 입력해주세요“를 출력하세요.

출력문

```
첫 번째 숫자 : 8
두 번째 숫자 : 4
4 5 6 7 8

첫 번째 숫자 : 4
두 번째 숫자 : 8
4 5 6 7 8

첫 번째 숫자 : 9
두 번째 숫자 : 0
1 이상의 숫자를 입력해주세요.
```

```js
// 내 답안
function practice4(input1, input2) {
  if (input1 >= 1 && input2 >= 1) {
    console.log('첫 번째 숫자 : ', input1);
    console.log('두 번째 숫자 : ', input2);
    if (input1 > input2) {
      for (let i = input2; i <= input1; i++) {
        console.log(i);
      }
    } else {
      for (let i = input1; i <= input2; i++) {
        console.log(i);
      }
    }
  } else {
    console.log('1 이상의 숫자를 입력해주세요.');
  }
}

// 다른 답안
function practice4(num1, num2) {
  if (!num1 || !num2 || isNaN(num1) || isNaN(num2) || num1 < 1 || num2 < 1) {
    console.log('1 이상의 숫자를 입력해주세요.');
    return;
  }

  console.log('첫 번째 숫자 : ', num1);
  console.log('두 번째 숫자 : ', num2);

  // 구조 분해할당(ES6) - JS에서 표준적인 swap 문장!
  if (num1 > num2) {
    [num1, num2] = [num2, num1];
  }

  let str = '';
  for (let i = num1; i <= num2; i++) {
    str += i + ' ';
  }
  console.log(str);
}
```

# Practice_06

## 문제 6

- 배열을 선언하고 1~10 사이의 정수형의 난수 10개를 배열에 넣은 후 출력하고 배열의 최대값과 최소값을 찾아 차례로 출력하세요.

```js
// 내 답안
function practice6() {
  const random = [];

  for (let i = 0; i < 10; i++) {
    random.push(Math.floor(Math.random() * 9 + 1));
  }
  random.sort((a, b) => a - b);
  console.log(random);
  console.log(`최대값 : ${random[random.length - 1]}`);
  console.log(`최소값 : ${random[0]}`);
}

// 다른 답안
function practice6() {
  let array = [];
  for (let i = 0; i < 10; i++) {
    array.push(Math.floor(Math.random() * 10 + 1));
  }
  console.log(array);

  console.log(`최대값 : ${Math.max(...array)}`);
  console.log(`최소값 : ${Math.min(...array)}`);
}
```

- 정렬은 인덱스 앞뒤의 값을 하나씩 비교해 가면서 반환하는 것이기 때문에 최소, 최대를 구할때 sort를 사용해 값을 구하는 것은 성능상 좋지 않다고 합니다.

# Practice_07

## 문제4

- money(ex : ₩ 1,952,477)는 사람들의 자산이다. 해당 자산을 모두 숫자로 변환하여 목록의 모든 사람의 모두 더한 값을 출력하세요.

### solution

```json
// json 파일 구조 총 20개의 객체로 이루어져 있어 19개는 생략하겠습니다..
{
  "_id": "c019cb5e-0673-47a7-Ab04-d5bd2c276097",
  "index": "1",
  "name": "문상욱",
  "email": "user1@test.com",
  "password": "373852",
  "gender": "남성",
  "phone": "010-2432-6371",
  "country": "모잠비크",
  "address": "논현로 83-2",
  "job": "기획자",
  "money": "￦ 3,332,202",
  "salary": "4988975",
  "bonus": "0.02"
}
```

```js
// 내 답안
function practice4() {
  let total = 0;
  let num = [];
  for (const obj of list) {
    let splitStr = obj.money.split('');

    let addItem = '';
    splitStr.map((item) => {
      if (item !== '￦' && item !== ' ' && item !== ',') {
        addItem += item;
      }
    });
    num.push(addItem);
  }
  for (let i = 0; i < num.length; i++) {
    total += Number(num[i]);
  }
  console.log(`합계 : ${total}원`);
}

// 다른 답안 1
function practice4() {
  let sum = 0;
  for (const obj of list) {
    money = obj.money.split(' ')[1];
    money = parseInt(money.replaceAll(',', ''));
    sum += money;
  }
  console.log(`합계 : ${sum}원`);
}

// 다른 답안 2 (정규실 풀이)
function practice4() {
  let sum = list.reduce((prev, cur) => prev + Number(cur.money.replaceAll(/\D/g, '')), 0);
  console.log('합계 : ' + sum + '원');
}
```

```toc

```
