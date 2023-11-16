---
emoji: 🖋
title: Canvas (2) 
date: '2023-03-30 16:50:00'
author: 중석 
tags: Js
categories: Js 
---
# 색상과 선 굵기 바꾸기 

# Html 


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meme Maker</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <canvas></canvas>
    <input id ="line-width" type="range" min="1" max="10" value="5" step="0.5">
    <div>
    <input type="color" id="color">
    <div
      class="color-option"
      style="background-color: #1abc9c"
      data-color="#1abc9c"
    ></div>
    <div
      class="color-option"
      style="background-color: #3498db"
      data-color="#3498db"
    ></div>
    <div
      class="color-option"
      style="background-color: #34495e"
      data-color="#34495e"
    ></div>
    <div
      class="color-option"
      style="background-color: #27ae60"
      data-color="#27ae60"
    ></div>
    <div
      class="color-option"
      style="background-color: #8e44ad"
      data-color="#8e44ad"
    ></div>
    <div
      class="color-option"
      style="background-color: #f1c40f"
      data-color="#f1c40f"
    ></div>
    <div
      class="color-option"
      style="background-color: #e74c3c"
      data-color="#e74c3c"
    ></div>
    <div
      class="color-option"
      style="background-color: #95a5a6"
      data-color="#95a5a6"
    ></div>
    <div
      class="color-option"
      style="background-color: #d35400"
      data-color="#d35400"
    ></div>
    <div
      class="color-option"
      style="background-color: #bdc3c7"
      data-color="#bdc3c7"
    ></div>
    <div
      class="color-option"
      style="background-color: #2ecc71"
      data-color="#2ecc71"
    ></div>
    <div
      class="color-option"
      style="background-color: #e67e22"
      data-color="#e67e22"
    ></div>
    </div>
    <script src="app.js"></script>
</body>
</html>
```

# style.css


```css
canvas {
    width:800px;
    height:800px;
    border:5px solid black;
}

body {
    display: flex;
    justify-content: center;
    align-items: center;
}
.color-option{
    width: 50px;
    height: 50px;
    cursor: pointer;
}
```

# app.js 


```js
const colorOptions = Array.from(
  document.getElementsByClassName("color-option")
);

function onLineWidthChange(event){
    ctx.lineWidth = event.target.value;
}

function onColorClick(event) {
  const colorValue = event.target.value;
  ctx.strokeStyle = colorValue;
  ctx.fillStyle = colorValue;
  color.value = colorValue;
}

function onColorOptionClick(event) {
   const colorValue = event.target.dataset.color;
  ctx.strokeStyle = colorValue;
  ctx.fillStyle = colorValue;
  color.value = colorValue;
}

colorOptions.forEach((color) => color.addEventListener("click", onColorOptionClick));

lineWidth.addEventListener("change", onLineWidthChange);
color.addEventListener("change", onColorClick);
```

## colorOptions

1. `cosnt = colorOptions` 를 배열로 바꾼것은 `forEach`를 사용해 
   각각의 `color-option` 의 `div` 에 `addEventListener` 를 주기 위함이다. 

2. `Array.from` 를 사용하지 않게 되면 `forEach` 는 `colorOptions`의 함수가 아니다 라는 로그를 볼 수 있을 것이다.

3. 즉 `forEach` 를 사용하기위해 `HTMLCollectiond` 의 `ArrayLike`객체인 
   `class=color-option` 을 배열로 바꿔주어야 한다. 

## onColorClick() 함수 

1. `const colorValue = event.target.value` 통해 `click`한 target의 색상을 `colorValue` 로 지정 

2. `ctx.strokeStyle = colorValue` 사용해 선의 색상을 지정해준다. 

3. `ctx.fillStyle = colorValue` 사용해 도형을 채우는 색상을 지정해준다. 

4. `color.value = colorValue` 사용해 현재 선택한 색상으로 바꿔준다. 

## onColorOptionClick() 함수 

 우리가 html에서 `class=color-option` 에 `data-color` 를 설정한걸 기억할 것입니다.
 
 `const colorValue = event.target.dataset.color` 를 통해서    
 우리가 click한 target의 data-color 값을 colorValue로 지정해 주었습니다. 

```toc

```