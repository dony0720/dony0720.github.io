---
emoji: 👨🏻‍💻
title: Day 33 useMemo, useCallback
date: '2025-01-12 00:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# useMemo

useMemo에서 memo는 memoization을 뜻하는데 이는 그대로 해석하면 ‘메모리에 넣기’라는 의미이며 컴퓨터 프로그램이 동일한 계산을 반복해야 할 때,
이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 반복 수행을 제거하여 프로그램 실행 속도를 빠르게 하는 기술이다.
즉, 동일한 값을 반환하는 함수를 반복적으로 호출해야한다면 처음 값을 계산할 때 해당 값을 메모리에 저장해 필요할 때마다 다시 계산하지 않고 메모리에서 꺼내서 재사용하는 것이다.
리액트에서 함수형 컴포넌트는 렌더링 => 컴포넌트 함수 호출 => 모든 내부 변수 초기화의 순서를 거친다.

메모이제이션: 기존에 수행한 연산의 결과값을 어딘가에 저장해두고 동일한 입력이 들어오면 재활용하는 프로그래밍 기법입니다.

```js
function Component() {
  const value = calculate();
  return <div>{value}</div>;
}

function calculate() {
  return 10;
}
```

만약에 calculate라는 함수가 매우 복잡한 로직으로 이루어져 있다고 가정해보자.
Component가 렌더링 될때마다 value는 calculate 함수를 실행시켜 값을 할당하게 되는 매우 비효율적인 상황이 발생하게 된다.
useMemo를 사용하게 된다면 이러 불필요한 상황을 줄일 수 있게 된다.

## useMemo 예시

```js
const value = useMemo(() => {
  return calculate();
}, [item]);
```

의존성 배열 안에있는 값이 업데이트 될 때에만 콜백 함수를 다시 호출하여 메모리에 저장된 값을 업데이트 해준다.
만약 빈 배열을 넣는다면 컴포넌트가 리렌더링되더라도 의존성 배열([])에 변경 사항이 없으므로 재계산되지 않고 기존 값을 재사용합니다.

참고 : https://velog.io/@jinyoung985/React-useMemo%EB%9E%80

# useCallback

useMemo가 결과값을 반환한다면 useCallback은 함수를 반환한다.

## 자식 컴포넌트에 props로 함수를 전달하는 경우

```js
import React, { useCallback, useState } from 'react';
import Profile from './Profile';

function App() {
  const [name, setName] = useState('');
  const onSave = useCallback(() => {
    console.log(name);
  }, [name]);

  return (
    <div className="App">
      <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
      <Profile onSave={onSave} />
    </div>
  );
}
```

useCallback을 사용하지 않을 경우

- name이 변경되어 리렌더링이 발생하면 onSave함수가 새로 만들어진다.
- Profile 컴포넌트의 props로 onSave함수가 새로 전달된다.
- 이때 Profile 컴포넌트에서 useMemo를 사용해도 이전 onSave와 이후 onSave가 같은 값을 반환하지만 참조가 다른 함수가 되어버리기 때문에 리렌더링이 일어나게 된다.

즉, 부모 컴포넌트만 수정하려고 했지만 연쇄적으로 하위 컴포넌트들 모두 렌더링이 일어나게된다.

## 외부에서 값을 가져오는 api를 호출하는 경우

```js
import React, { useState, useEffect } from 'react';

function Profile({ userId }) {
  const [user, setUser] = useState(null);

  const fetchUser = useCallback(
    () =>
      fetch(`https://your-api.com/users/${userId}`)
        .then((response) => response.json())
        .then(({ user }) => user),
    [userId],
  );

  useEffect(() => {
    fetchUser().then((user) => setUser(user));
  }, [fetchUser]);

  // ...
}
```

useCallback 사용하지 않을 경우

- Profile이라는 컴포넌트가 리렌더링이 발생할 경우 fetchUser 함수에는 새로운 함수가 할당된다.
- 그러면 useEffect()함수가 호출되어 user 상태값이 바뀌고, state 값이 바뀌었기 때문에 다시 리렌더링이 일어난다.

즉, 불필요한 리렌더링이 한번 더 발생된다. 그래서 useCallback을 사용하게 되면 userId가 변동될 때만 fetchUser에 새로운 함수가 할당되도록 설정하고,
그것이 아니면 동일한 함수가 실행되게 되서 불필요한 리렌더링을 방지할 수 있다.

참고 : https://narup.tistory.com/273#google_vignette

```toc

```
