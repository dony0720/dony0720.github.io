---
emoji: 📝
title: React (2)
date: '2023-12-26 16:30:00'
author: 중석
tags: React
categories: React
---

## MinutesToHours 컴포넌트 함수

```js
const root = document.querySelector("#root");
      function MinutesToHours() {
        const [amount, setAmount] = React.useState(0);
        const [flipped, setFliped] = React.useState(false);
```

### 배열 비구조화 할당

1. amount는 React.useState(0)을 사용해 초기값을 0으로 설정,  
   flipped는 React.useState(false) 초기값을 false로 설정 하게된다.
2. setAmount, setFliped 함수는 amount와 flipped의 값을 업데이트 할때 사용된다.

```js
const onChange = () => {
  setAmount(event.target.value);
};
const reset = () => setAmount(0);
const onFlip = () => {
  reset();
  setFliped((current) => !current);
};
```

1. setFliped(counter + 1)로 로직을 만들 경우 counter는 state를 할당한 값만 참조한다.  
   즉, setFliped를 여러번 호출하게 되면 값이 항상 2가 된다.

2. 하지만 setFliped((current) => !current)로 로직을 만들 경우 current에는 useStete의 state자체를 참조한다.  
   여러번 함수를 호출하게 되면 값을 업데이트해서 반영한다.

```js
return (
          <div>
            <div>
              <label htmlFor="minutes">Minutes</label>
              <input
                value={flipped ? amount * 60 : amount}
                /* 
                삼항 연산자를 사용해서 flipped가 true일때는 amount * 60의 값을 반영,    
                false일때는 amount 의 값을 반영한다. 
                */
                id="minutes"
                placeholder="Minutes"
                type="number"
                onChange={onChange}
                disabled={flipped}
              />
            </div>

            <div>
              <label htmlFor="hours">Hours</label>
              <input
                value = {flipped ? amount : Math.round(amount / 60)}
                id="hours"
                placeholder="Hours"
                type="number"
                onChange={onChange}
                disabled={!flipped}
              />
            </div>
            <button onClick={reset}>Reset</button>
            <button onClick={onFlip}>Flip</button>
          </div>
        );
      }
```

React에서는 Jsx문법을 Javascript로 변환하기 때문에 따로 Javascript를 쓰기 위해서는 {}를 사용해 주어야 한다.

## App 컴포넌트 함수 

```js
function App() {
        const [index, setIndex] = React.useState("xx");
        const onSelect = (event) => {
          setIndex(event.target.value);
        };
        //setIndex 함수를 이용해서 해당 옵션의 value 값을 index의 값으로 업데이트 한다. 

        return (
          <div>
            <h1>Super Converter</h1>
            <select onChange={onSelect}>
              <option value="xx">Select your units</option>
              <option value="0">Minutes & Hours</option>
              <option value="1">Km & miles</option>
            </select>
            {/*옵션을 선택할때마다 변화를 감지해서 onSlelct 함수가 동작하게 된다.*/}
            
            <hr />
            {index === "xx" ? <h3>"Please select your units"</h3> : null}
            {index === "0" ? <MinutesToHours /> : null}
            {index === "1" ? <KmToMiles /> : null}
            {/*index의 비교되는 값과 같을때 ? 뒤에 있는 텍스트나 컴포넌트를 렌더링한다.*/}
          </div>
        );
      }
```
```toc

```