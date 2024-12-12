---
emoji: 👨🏻‍💻
title: WTL 3회차 이벤트 루프, 콜스택, 마이크로태스크 큐, 매크로태스크 큐- 1차 프로젝트 5팀
date: '2024-12-12 22:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 이벤트루프

- 태스크가 오길 기다렸다가 태스크가 들어오면 이를 처리하고, 처리할 태스크가 없는 경우엔 잠드는, 끊임없이 돌아가는 자바스크립트 내 루프입니다.
- 자바스크립트는 싱글 스레드 기반의 언어(작업을 한개씩 처리)며, 자바스크립트 엔진은 하나의 콜 스택만 사용합니다.

## 이벤트 루프의 필요성

자바스크립트는 싱글 스레드 언어로 작업을 한개씩 처리한다고 합니다. 하지만 실제 개발에서는 동시에 작업이 이루지는 것을
볼 수 있습니다. 그 이유는 바로 **이벤트 루프** 라는 장치가 있기 때문입니다.
웹 사이트나 애플리케이션의 코드는 메인 스레드에서 실행되며, 같은 이벤트 루프를 공유합니다.

메인 스레드의 역할 : 1. 코드 실행, 2. 이벤트를 받고 실행, 3. 웹 컨텐츠 렌더링과 페인팅

## 브라우저 환경의 구조

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdzxj66%2FbtrG8t1ZiKI%2FAHzF6VNt1sihtkwLKQN0B1%2Fimg.png)

- Heap : 객체들은 힙 메모리에 할당됩니다.
- 콜스택 : 함수 호출시 실행컨텍스트가 생성되며, 실행컨텍스트들이 콜스택을 구성합니다
- Web API or Browser API : 웹 브라우저에 구현된 API, 예시 - DOM event, AJAX, Timer 등이 있습니다.
- 이벤트 루프 : 콜스택이 비어있다면, 태스크 큐에 있는 콜백 함수를 처리합니다.
- 태스크 큐 : 작업(Task)을 순차적으로 처리하기 위해 사용하는 **대기열(queue)** 입니다

## 마이크로 태스크 & 매크로 태스크

두 비동기 작업들을 처리하는 방법들로 비동기 작업들은 태스크 큐라는 저장공간에 들어가게 됩니다. 태스크 큐는 발생한 순서대로 큐에 쌓이고 이벤트 루프에 의해 처리되며 태스크큐는 매크로 태스크 큐 와 마이크로 태스크로 구분할 수 있는데, 이 둘의 차이는 처리할 작업의 우선순위 입니다. 마이크로 태스크는 매크로 태스크 보다 우선순위가 높습니다. **그렇기 때문에 항상 마이크로태스크의 작업이 더 먼저 처리됩니다.**

## 매크로와 마이크로에 속하는 작업들

- 매크로 태스크(macroTasks) - DOM 이벤트 콜백, 타이머(setTimeout, setInterval), 스크립트 로딩, requestAnimationFrame 등

  - requestAnimationFrame : 브라우저에게 수행하기를 원하는 애니메이션을 알리고 다음 리페인트 바로 전에 브라우저가 애니메이션을 업데이트할 지정된 함수를 호출하도록 요청하는 메서드입니다.

- 마이크로태스크(microTasks) - 프로미스(Promises) 핸들러 (then / catch / finally) + await, (MutationObserver 등)

## 이벤트 루프 동작 방식

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwBXB5%2FbtrG7XCi7RX%2Fzda2mCgMntycvgkcqBspR1%2Fimg.png)

```js
console.log('Start');

setTimeout(() => {
  console.log('TimeOut');
}, 0);

Promise.resolve('Promise1!').then(() => console.log('Promise1!'));
Promise.resolve('Promise2!').then(() => console.log('Promise2!'));
console.log('End');
```

```
출력값

Start
End
Promise!
TimeOut
```

그림과 함께 위 코드에 대해서 설명하고자 합니다.

### 콜스택 처리

1. 호출스택(콜스택)이 비었는지 지속적으로 확인합니다.
2. `console.log('Start');`가 호출스택에 쌓여서 실행하게 됩니다.
3. 다음으로 콜스택에 setTimeout 함수가 쌓여서 `() => {console.log('TimeOut')}`을 Web API로 보냅니다.
4. Web API에서 setTimeout의 콜백인 `() => {console.log('TimeOut')}`을 매크로태스크 큐에 보냅니다.
5. 콜스택에 `Promise.resolve() -> then(() => console.log("Promise1"))`의 순서로 쌓이게 됩니다.

   ```
   호출 스택

   then(() => console.log("Promise1"))
   ------------------------------------
   Promise.resolve()
   ```

6. 콜스택에서 `then(() => console.log(Promise1))`를 마이크로 큐에 보냅니다.
7. 콜스택에 `Promise.resolve() -> then(() => console.log("Promise2"))`의 순서로 쌓이게 됩니다.
8. 콜스택에서 `then(() => console.log(Promise2))`를 마이크로 큐에 2번재로 보냅니다.
9. 마지막 코드인 `console.log('End');`를 실행합니다.

### 태스크 처리

```
마이크로태스크 큐

 () => console.log("Promise1") -> () => console.log("Promise2")

매크로태스크 큐

    () => {console.log('TimeOut')}
```

1. 이벤트 루프는 태스크들을 처리하기 위해 호출 스택이 비었는지 계속 확인하며 호출 스택이 비었다면, 이벤트 루프는 가장 먼저 마이크로 태스크 큐에 쌓여있는 태스크들을 () => console.log("Promise1") -> () => console.log("Promise2") 의 순서로 처리합니다.

2. 매크로 태스크 큐를 처리하기 전에 UI 렌더링 작업이 필요하면 렌더링을 이때 수행합니다.

3. 이제 매크로태스크 큐를 처리하고 다시 마이크로태스크 큐가 쌓여있는지 확인합니다. 만약 쌓여 있다면 태크크 처리의 1번 과정부터 다시 진행하게 됩니다.

4. ✨필수 개념✨ : 브라우저는 매크로태스크 하나를 처리할 때마다 마이크로 태스크 전부를 다 처리하고 렌더링을 수행한다는 것입니다. 그래서 마이크로태스크가 모두 처리되기 전까지는 UI 렌더링이나 네트워크 요청은 절대 일어나지 않습니다.

참고 : https://talkwithcode.tistory.com/89  
참고 : https://whales.tistory.com/130  
참고 : https://ko.javascript.info/event-loop#ref-436

```toc

```
