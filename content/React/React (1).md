---
emoji: 📝
title: React 
date: '2023-11-02 15:30:00'
author: 중석 
tags: React
categories: React  
---

# React Js란?
React JS는 기본적으로 Facebook에서 구축하고 유지 관리하는 JavaScript 라이브러리입니다.   
또한 웹 애플리케이션의 간단하고 빠르며 확장 가능한 프런트엔드를 구축하기 위한 효율적이고    
선언적이며 유연한 오픈 소스 JavaScript 라이브러리입니다.

# Jxs란?
+ JavaScript에 XML을 추가하여 확장한 문법이다. 


## React Js 필요한 스크립트 태크
```js
  <body>   
    <div id="root"></div>   
    <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script> 
    <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
```
React Js를 설치하기 위한 JavaScript 코드 
```js
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/babel">
```
 Jsx 문법을 브라우저가 이해할 수 있는 형태로 변환하기 위해 필요하다

## 컴포넌트 작성 
```js
const Title = () => (
    <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
        Hello I'm a title
    </h3>
);

const Button = () => (
    <button
        style={{
            backgroundColor: "tomato",
        }}
        onClick={() => console.log("im clicked")}
    >
        Click me
        </button>
);


```
### 함수형 컴포넌트 선언  

    1. 컴포넌트 작성시 무조건 대문자로 시작! 
    2. 함수형 컴포넌트 선언 방법 
      1) const Title = () => () , 화살표 뒤에 ()로 감싸는 경우는 return을 전제로 한다. 
      2) function = () => {return()}, 화살표 뒤에 {}로 감싸는 경우는    
         return을 안한다는걸 전제로 하기 때문에 따로 return을 해주어야한다. 
 
    3. 선언된 컴포넌트 안에는 html과 같이 태그안에 속성, 이벤트, 내용을 적어주면 된다.

## 렌더링 
```js
const Container = () => (
    <div>
        <Title />
        <Button />
    </div>
);
```

1. Container에 Title과 Button을 포함시키기 위해서는 function으로 만들어주어야 함
2. 선언한 컴포넌트를 불러오기 위해서는 `<컴포넌트 이름>` 형태로 작성해주면 된다. 
  
```js
ReactDOM.render(<Container />, root);
```
1. 작성한 jsx를 화면에 렌더링하기 위한 함수 
2. 컴포넌트를 페이지에 렌더링하는 역할을 하며, react-dom 모듈을 불러와야 사용가능하다.
3. `<Container />`는 Jsx로 작성된 컴포넌트를 의미, `root`는 작성된 Container 컴포넌트를 렌더링해서 보여줄 DOM 안의 위치를 의미한다 
4. `<Container />`를 render 시키기 위해서는 Container 컴포넌트도 함수로 만들어줘야함
      
## React JS와 Vanilla JavaScript의 노드 변경 차이점 

### Vanilla JavaScript
Vanilla JavaScript에서는 DOM 변경을 직접 처리한다.   
즉, 필요한 DOM 요소를 직접 선택하고, 요소의 속성을 변경하거나    
새로운 요소를 추가하거나 기존 요소를 제거하는 등의 작업을 직접 수행하게 된다.   
DOM 변경이 발생하면, 브라우저는 변경된 DOM 트리를 다시 계산하고,    
렌더 트리를 다시 생성한 후 화면에 그린다.    
이 과정은 비용이 많이 드는 연산으로, 자주 발생하게 되면 성능을 저하시킬 수 있다고 한다.


### React JS
ReactJS는 DOM 변경을 처리하기 위해 가상 DOM(Virtual DOM)이라는 개념을 도입한다.    
ReactJS에서는 먼저 메모리에 가상 DOM 트리를 생성한다.    
이 트리는 실제 DOM 트리의 사본으로서, 실제 DOM 트리와 별도로 존재한다.   
ReactJS는 상태 변경이 발생할 때마다 새로운 가상 DOM 트리를 생성하고,    
이전의 가상 DOM 트리와 비교하여 변경된 부분을 파악한다.   
이렇게 파악된 변경 사항만 실제 DOM에 반영하는 방식을 사용한다.   
이 과정을 '재조정(Reconciliation)' 또는 'Diffing'이라고 부른다.   
가상 DOM을 사용함으로써, 변경이 필요한 최소한의 요소만 실제 DOM에 반영되기 때문에    
불필요한 연산을 줄이고 성능을 향상시킬 수 있다고 한다.