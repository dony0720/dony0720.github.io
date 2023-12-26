---
emoji: 📝
title: React (3)
date: '2023-12-26 17:30:00'
author: 중석
tags: React
categories: React
---

# Props란?

1. 부모 컴포넌트로부터 자식 컴포넌트에게 데이터를 보내주는 방법
2. 객체이다.

```js
<script src="https://unpkg.com/react@17.0.2/umd/react.development.js "></script>
```

어떤 prop들을 받는지 검사하게끔 도와주는 역할을 한다.

## Btn 컴포넌트 함수

```js
function Btn({ text, fontSize }) {
  return (
    <button
      style={{
        backgroundColor: 'tomato',
        color: 'white',
        padding: '10px 20px',
        border: 0,
        borderRadius: 10,
        fontSize,
      }}
    >
      {text}
    </button>
  );
}
```

1. props는 객체이기 때문에 { }열어 원하는 속성을 바로 받을 수 있음
2. { }를 사용하지 않게 되면 props.text, props.fontSize의 방식으로 값에 접근해야한다.

```js
Btn.propTypes = {
  text: propTypes.string.isRequired,
  fontSize: propTypes.number,
};
```

text prop은 string 형태의 데이터, fontSize는 number 형태의 데이터가 아닐시 동작은 되지만  
콘솔 창에 올바른 형태의 데이터가 아니라고 경고를 알려준다.

## App 컴포넌트 함수

```js
function App() {
  return (
    <div>
      <Btn text="save" fontSize={18} />
      <Btn text="Continue" />
    </div>
  );
}

ReactDOM.render(<App />, root);
```

1. 어떠한 것들을 컴포넌트 안에 넣든간에 HTML안에 영향을 주지 않고 prop이 된다.
2. 컴포넌트 함수에 해당 prop을 등록하고 작성해야만 한다.
3. 전달된 prop들은 하나의 오브젝트로 받게된다.
4. prop을 전달할때의 이름과 받아서 사용할때의 이름은 동일해야한다.

## props와 stata의 차이점 
1. props: 함수의 매개변수처럼 컴포넌트에 전달된다. 
2. state: 함수 내에 선언된 변수처럼 컴포넌트 안에서 관리된다. 