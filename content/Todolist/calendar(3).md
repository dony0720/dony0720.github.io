---
emoji: 🧢
title: TodoList (8) - Calendar 기능 구현(2)
date: '2023-03-28 16:20:00'
author: Js 
tags: TodoList 작성 
categories: TodoList Js 
---
# Calendar 버튼 기능 구현 

## 소스코드 


```js
const goPre = document.querySelector(".go-pre");
const goNext = document.querySelector(".go-next");
const goTd = document.querySelector(".go-today")
function preMonth() {
  dt.setMonth(dt.getMonth() - 1)
  renderCalendar();
}

function nextMonth() {
  dt.setMonth(dt.getMonth() + 1)
  renderCalendar();
}

// element.setMonth(element.getMonth())는 12월이 넘어갈때 자동으로 연도가 바뀜  

function todaybtn(){
  dt = new Date();
  renderCalendar();
}

renderCalendar()

goPre.addEventListener("click", preMonth);
goNext.addEventListener("click", nextMonth);
goTd.addEventListener("click", todaybtn);
```
<br>

## preMonth() 함수 


```js
function preMonth() {
  dt.setMonth(dt.getMonth() - 1)
  renderCalendar();
}
```

+ **'<' 버튼을** 누를때 이전달로 넘어가야 하기 때문에 

+ `dt.setMonth(dt.getMonth() - 1)` 를 이용해 현재 달에 -1 값으로 설정  

+ 재할당된 dt.setMonth를 가지고 renderCalendar() 호출

<br>

## nextMonth() 함수 


```js
function nextMonth() {
  dt.setMonth(dt.getMonth() + 1)
  renderCalendar();
}
```

+ **'>'버튼을** 누를때 다음달로 넘어가야 하기 때문에 

+ `dt.setMonth(dt.getMonth() + 1)` 를 이용해 현재 달에 +1 값으로 설정

+ 재할당된 `dt.setMonth`를 가지고 `renderCalendar()` 호출

<br>

## todaybtn() 함수 


```js
function todaybtn(){
  dt = new Date();
  renderCalendar();
}
```

+ Today 버튼을 누를때 다시 현재 날짜로 돌아오기 위해 dt의 값을    
  `new Date()`로 할당해야기 때문에 **초반에 dt 를 `const`가 아닌 `let`으로 설정한이유** 
