---
emoji: 📝
title: Redux에 대해서
date: '2025-06-05 10:05:00'
author: 중석
tags: React
categories: React
---

# Redux란?

리덕스는 가장 많이 사용하는 리액트 상태 관리 라이브러리이다.
리덕스를 사용하면 컴포넌트의 상태 업데이트 관련 로직을 다른 파일로 분리시켜 효율적을 관리가 가능하고
Props 없이 다른 컴포넌트에게도 상태를 전달할 수 있다.
하지만 단순히 전역 상태 관리만 하는 프로젝트라면 Context API로 충분하다고 한다.

## Redux 개념(1) - Action(액션)

Redux에서 **"액션(action)"** 은 상태(state)를 어떻게 바꿔야 하는지를 설명하는 **"객체"** 다.  
말 그대로, “이런 일이 일어났다”고 리덕스에 알리는 역할을 한다.

액션은 무조건 객체이며, 필수로 type 속성을 가져야 한다.

```js
{
  type: 'counter/increment'
}
// payload가 있는 경우
{
  type: 'counter/incrementByAmount',
  payload: 5 // 상태 업데이트에 필요한 추가 정보를 포함
}

```

## Redux 개념(2) - Action Creator(액션 생성 함수)

**액션 생성 함수(Action Creator)** 는 액션 객체를 반환하는 함수입니다.

### 왜 액션 생성 함수를 쓸까?

1. 코드 일관성 유지 - 액션 객체를 직접 만들지 않고, 공통된 방식으로 생성 가능
2. 자동화/ 테스트 용이 - 함수로 분리되어 테스트하기 쉬움
3. 실수 방지 - 오타나 잘못된 구조를 줄일 수 있음

```js
function increment() {
  return {
    type: 'counter/increment',
  };
}

// 화살표 함수 예시
const increment = () => {
  return {
    type: 'counter/increment',
  };
};
```

## Redux 개념(3) - Reducer(리듀서)

리듀서는 변화를 일으키는 함수이다. 액션을 만들어서 발생시키면 리듀서가 현재 상태와 전달받은 액션 객체를 파라미터로 받아서 새로운 상태를 만들어 반환해준다.

```js
const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case 'counter/increment':
      return state + 1;
    case 'counter/incrementByAmount':
      return state + action.payload;
    default:
      return state;
  }
};
```

## Redux 개념(5) - DisPatch(디스패치)

디스패치는 스토어의 내장 함수 중 하나이다. dispatch 함수는 액션을 스토어에 보내는 데 사용된다.
액션이 디스패치되면 스토어는 리듀서를 호출하여 새로운 상태를 계산한다.

## Redux 개념(6) - Subscribe(구독)

구독도 스토어의 내장 함수 중 하나이다. subscribe 함수 안에 리스너 함수를 파라미터로 넣어서
호출해 주면, 이 리스너 함수가 액션이 디스패치되어 상태가 업데이트될 때마다 호출된다.

```js
const listener = () => {
  console.log('updated!');
};
const unsubscribe = store.subscribe(listener);

unsubscribe(); // 구독 비활성화 시 함수 호출
```

- store.subscribe(listener)를 호출하면 listener 함수가 스토어의 상태가 변경될 때마다 호출되도록 구독을 설정한다.  
  즉, 스토어의 상태가 변경될 때마다 listener가 실행된다.
- 구독 해제 함수 반환: store.subscribe(listener)는 구독을 해제할 수 있는 함수를 반환한다.  
  이 반환된 함수를 unsubscribe 변수에 저장한다.  
  나중에 unsubscribe()를 호출하면 해당 구독이 해제되어 더 이상 listener가 호출되지 않게 된다.

## Redux Toolkit에 대해서

**Redux Toolkit** 은 Redux의 공식 권장 도구 세트로,
복잡하고 반복적인 Redux 설정을 간단하고 효율적으로 만들어준다.

### configureStore

Redux 스토어를 설정하는 데 사용된다. 미들웨어, 리듀서, DevTools 설정 등을 자동으로 구성해준다.

```js
import { configureStore } from '@reduxjs/toolkit';
import rootReducer from './reducers';

const store = configureStore({
  reducer: rootReducer,
});
```

### createSlice

리듀서와 액션 생성 함수를 함께 정의할 수 있는 기능을 제공합니다. 이를 통해 보일러플레이트 코드를 줄이고, 코드의 일관성을 유지할 수 있습니다.
createSlice는 자동으로 액션 타입과 액션 생성 함수를 생성합니다.

- 보일러플레이트(boilerplate): 소프트웨어 개발에서 반복적으로 사용되는 코드의 템플릿이나 기본 구조를 의미한다.

```js
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment(state) {
      state.value += 1; // 불변성 걱정 없음!
    },
    decrement(state) {
      state.value -= 1;
    },
  },
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

### createAsyncThunk

비동기 로직을 처리하기 위한 유틸리티로, 비동기 액션을 생성하고 상태를 관리하는 데 도움을 준다.
API 호출과 같은 비동기 작업을 쉽게 처리할 수 있도록 설계되었다.

```js
import { createAsyncThunk } from '@reduxjs/toolkit';

export const fetchUser = createAsyncThunk('users/fetchUser', async (userId, thunkAPI) => {
  const response = await fetch(`/api/user/${userId}`);
  return response.json();
});
```

### createEntityAdapter

일반적인 CRUD 작업을 쉽게 수행할 수 있도록 도와주는 유틸리티이다.
엔티티의 상태를 관리하고, 정렬 및 필터링을 쉽게 할 수 있도록 도와준다.

### immer

Redux Toolkit은 내부적으로 immer를 사용하여 불변성을 유지하면서 상태를 쉽게 업데이트할 수 있도록 한다.
이를 통해 복잡한 상태 업데이트 로직을 간단하게 작성할 수 있다.
