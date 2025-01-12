---
emoji: 👨🏻‍💻
title: Day 32 useContext, useReducer
date: '2025-01-09 22:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# useContext

Context는 앱 안에서 전역적으로 사용되는 데이터를 여러 컴포넌트끼리 쉽게 공유할 수 있는 방법을 제공한다.
Context를 사용하면 Props로 데이터를 일일이 전달해 주지 않아도 해당 데이터를 가지고 있는 상위 컴포넌트에 그 데이터가 필요한 하위 컴포넌트가 접근할 수 있다.
즉 사용자 정보, 테마, 언어 등 전역적인 데이터를 전달하기에 정말 편리하다.
상위 컴포넌트의 data가 필요한 하위 컴포넌트들은 useContext 훅을 사용해서 해당 데이터를 받아오기만 하면 된다.
useContext는 Context로 분류한 데이터를 쉽게 받아올 수 있게 도와주는 역할을 한다.

## 🚨 주의 사항

context는 꼭 필요할 때만 사용한다. context를 사용하면 컴포넌트를 재사용하기 어려워질 수 있다.
context의 주된 목적인 다양한 레벨이 있는 많은 컴포넌트들에게 전역적인 데이터를 전달하기 위함이다.
리액트 공식 문서에는 context를 사용하는 이유가 단지 prop drilling(중첩된 컴포넌트를 거쳐 데이터를 전달하는 것)을 피하기 위한 목적이라면
component composition(컴포넌트 합성)이 더 간단한 해결책이라고 제시하고 있다.

## state와 props만 사용

### App 컴포넌트

```js
// 최상위 컴포넌트
import { useState } from 'react';
import './App.css';
import Page from './Components/Page';

function App() {
  // 햔제 App 이 다크모드인지 아닌지 true false 로 정보를 받고 있다.
  const [isDark, setIsDark] = useState(false);

  // Page 자식 컴포넌트에게 해당 데이터를 props로 넘겨 주고 있다.
  return <Page isDark={isDark} setIsDark={setIsDark} />;
}
export default App;
```

### Page 컴포넌트

```js
// page 컴포넌트
import React, { useContext } from 'react';
import Content from './Context';
import Header from './Header';
import Footer from './Footer';

const Page = ({ isDark, setIsDark }) => {
  return (
    <div className="page">
      <Header isDark={isDark} />
      <Footer isDark={isDark} setIsDark={setIsDark} />
    </div>
  );
};
```

### Header 컴포넌트

```js
import React from 'react';

const Header = ({ isDark }) => {
  return (
    <header
      className="header"
      style={{
        backgroundColor: isDark ? 'black' : 'lightgray',
        color: isDark ? 'white' : 'black',
      }}
    >
      <h1>Welcome 홍길동</h1>
    </header>
  );
};

export default Header;
```

### Footer 컴포넌트

```js
import React from 'react';

const Footer = ({ isDark, setIsDark }) => {
  const toggleTheme = () => {
    setIsDark(!isDark);
  };
  return (
    <footer className="footer" style={{ backgroundColor: isDark ? 'black' : 'lightgray' }}>
      <button className="button" onClick={toggleTheme}>
        Dark Mode
      </button>
    </footer>
  );
};

export default Footer;
```

- App 컴포넌트가 가지고 있는 isDark, setIsDark를 Page 컴포넌트를 통해 하위 (Header, Footer)에 넘겨주게 된다.
- Page 컴포넌트는 isDark, setIsDark를 받아는 오지만 실질적으로 사용하지 않고 있다. 즉, 즉, 본인(Page)에게 필요없는 props를 가진 중간 컴포넌트다.

## useContext 사용

### ThemeContext.js

ThemeContext.js라는 파일을 만들고 아래 코드를 작성한다

```js
import { createContext } from 'react';

// 기본값으로는 null을 넣어준다.
export const ThemeContext = createContext(null);
```

### App 컴포넌트

```js
import { useState } from 'react';
import './App.css';
import Page from './Compopnents/Page';
import { ThemeContext } from './context/ThemeContext';

function App() {
  const [isDark, setIsDark] = useState(false);

  return (
    // 📌
    <ThemeContext.Provider value={{ isDark, setIsDark }}>
      <Page />
    </ThemeContext.Provider>
  );
}
export default App;
```

- ThemeContext.js에 작성된 파일을 App 컴포넌트에 import 시킨다.

### Page 컴포넌트

```js
import React from 'react';
import Content from './Context';
import Header from './Header';
import Footer from './Footer';

const Page = () => {
  return (
    <div className="page">
      <Header />
      <Content />
      <Footer />
    </div>
  );
};

export default Page;
```

- isDark 를 실질적으로 사용하지 않고, 자녀 컴포넌트들에게 전달하는 역할
- data가 필요하지 않다.

### Header 컴포넌트

header에서는 props를 지워주고 useContext 훅을 사용해 ThemeContext를 불러온다.

```js
import { useContext } from 'react';
// 📌
import { ThemeContext } from '../context/ThemeContext';

const Header = () => {
  // 📌
  const { isDark } = useContext(ThemeContext);
  return (
    <header
      className="header"
      style={{
        backgroundColor: isDark ? 'black' : 'lightgray',
        color: isDark ? 'white' : 'black',
      }}
    >
      <h1>Welcome 홍길동!</h1>
    </header>
  );
};

export default Header;
```

### Footer 컴포넌트

```js
import React, { useContext } from 'react';
import { ThemeContext } from '../context/ThemeContext';

const Footer = () => {
  // 📌
  const { isDark, setIsDark } = useContext(ThemeContext);
  const toggleTheme = () => {
    setIsDark(!isDark);
  };
  return (
    <footer className="footer" style={{ backgroundColor: isDark ? 'black' : 'lightgray' }}>
      <button className="button" onClick={toggleTheme}>
        Dark Mode
      </button>
    </footer>
  );
};

export default Footer;
```

## 정리

App 컴포넌트에서 context를 불러와서 모든 하위 컴포넌트에게 알린 것이라고 할 수 있다.
page 컴포넌트는 해당 데이터가 필요하지 않으니까 context를 쓸 필요가 없고,
page의 자식 컴포넌트는 해당 데이턱 필요하니 useContext 훅을 사용해서 해당 전역 데이터에 접근한 것이다.

참고 : https://velog.io/@hjthgus777/React-%EB%8B%A4%EC%8B%9C-%ED%95%9C%EB%B2%88-useContext%EB%A5%BC-%ED%8C%8C%ED%97%A4%EC%B3%90%EB%B3%B4%EC%9E%90

# useReducer

useReducer는 useState의 대체재로, 상태가 복잡하거나 여러 상태가 서로 의존할 때 useReducer를 활용된다. ( Redux와 사용 패턴 유사 )

## useReducer 사용 방법

```js
import { useReducer } from 'react';

function createInitialState(username) {
  const initialTodos = [];
  for (let i = 0; i < 20; i++) {
    initialTodos.push({ id: i, text: username + "'s task #" + (i + 1) });
  }

  // state 구조!
  return {
    draft: '', // 문자열
    todos: initialTodos, // object 배열
  };
}

function reducer(state, action) {
  switch (action.type) {
    case 'added_todo': {
      return {
        draft: '',
        todos: [{ id: state.todos.length, text: state.draft }, ...state.todos],
      };
    }
    case 'changed_draft':
      return { draft: action.nextDraft, todos: state.todos };
    default:
      throw new Error('Unknown action: ' + action.type);
  }
}

// TodoList 예제
export default function UseReducer({ username }) {
  const [state, dispatch] = useReducer(reducer, username, createInitialState);
  return (
    <>
      <input
        value={state.draft}
        onChange={(e) => {
          dispatch({ type: 'changed_draft', nextDraft: e.target.value });
        }}
      />
      <button
        onClick={() => {
          dispatch({ type: 'added_todo' });
        }}
      >
        Add
      </button>
      <ul>
        {state.todos.map((item) => (
          <li key={item.id}>{item.text}</li>
        ))}
      </ul>
    </>
  );
}
```

### reducer 함수

상태(state)를 업데이트하는 역할을 한다. 액션(action) 타입에 따라 상태를 업데이트하는 로직을 정의한다.

- type이 "added_todo" 일 경우

  - 새로운 Todo를 추가한다.
  - 새로운 Todo의 text는 현재 draft 값을 사용하며, 새 Todo는 기존 todos 배열의 맨 앞에 추가된다.
  - draft는 빈 문자열로 초기화됩니다.

- type이 "changed_draft"일 경우

  - 사용자가 입력 필드에서 입력한 값을 draft로 업데이트한다.

- 기본(default)

  - 정의되지 않은 액션 타입이 전달되면 에러를 던집니다.

### UseReducer

1. 초기 상태 생성

```js
const [state, dispatch] = useReducer(reducer, initialArg, initFunction);
```

- state: 현재 상태 값이다.
- dispatch: 상태를 업데이트하기 위한 함수다.

- reducer (상태 업데이트 로직)
- initialArg (초기 상태 계산에 사용될 값)
- initFunction (선택적으로 초기 상태를 동적으로 계산)

2. 내부 동작 흐름

- 초기 상태 계산 : initFunction 있다면 호출한다.

```js
const initialState = initFunction ? initFunction(initialArg) : initialArg;
```

- state 초기화: state는 initialState로 설정한다.
- dispatch 생성: dispatch는 reducer와 연결한다.

```js
const [state, dispatch] = useReducer(reducer, username, createInitialState);
```

3. 입력 필드와 버튼

   input 필드

   - value: state.draft 값을 바인딩합니다.
   - onChange: 사용자가 입력한 값을 dispatch를 통해 "changed_draft" 액션으로 상태를 업데이트합니다.

   button

   - 클릭하면 "added_todo" 액션을 dispatch하여 현재 draft 값을 새로운 Todo로 추가합니다.

```toc

```
