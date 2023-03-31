---
emoji: 🖋
title: Canvas 1 
date: '2023-03-30 16:50:00'
author: Js 
tags: Canvas를 이용한 그림판
categories: Canvas Js 
---
# Canvas를 이용한 그림판 

## Html 구조 소스코드 


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
    </div>
    <button id = "mode-btn">fill</button>
    <button id = "Erase-btn">Erase</button>
    <button id = "Reset-btn">Reset</button>
    <input type="file" accept="image/*" id ="file">
    <input type="text" id="text" placeholder="Write and then double click">
    <button id ="save">save</button>
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
```

# app.js (1) 


```js
const canvas = document.querySelector("canvas");
const ctx = canvas.getContext("2d"); //브러쉬 역할 => 2d,webgl,bitmaprederer의 옵션이 있음 
let isPainting = false;
canvas.width = 800;
canvas.height = 800;
const lineWidth = document.getElementById("line-width");

ctx.moveTo(0,0); //시작점을 0,0으로 설정 
ctx.lineWidth = lineWidth.value; // 선의 굵기를 조정 

function startPainting() {
  isPainting = true;
}

function cancelPainting() {
  isPainting = false;
  ctx.beginPath();
}

function onMove(event) {
    if (isPainting) {
      ctx.lineTo(event.offsetX, event.offsetY); //다음지점으로 선을 연결시킴 
      ctx.stroke(); // 윤곽선을 생성  
      return;
    }
    ctx.moveTo(event.offsetX, event.offsetY);
  }

modeBtn.addEventListener("click", onModeClick);
canvas.addEventListener("mousedown", startPainting);
canvas.addEventListener("mouseup", cancelPainting);
```

## onMove() 함수 

1. `mousedown`이 될때 `addEventListener`를 통해 `isPainting = true`
   onMove함수의 참 부분이 실행된다. 

2. 함수의 event인자는 현재 click 되어지고있는 지점이다.
    
    + click = mousedown 후에 mouseup이 되어야한다. 
    
    + mousedown = 마우스버튼 내리기 
    
    + mouseup = 마우스버튼 올리기    
    
3. **`ctx.lineTo(event.offsetX, event.offsetY)`** 를 통해 다음지점으로 선을 연결시킨다. 

4. **`ctx.stroke()`** 통해 연결한 선을 채운다. 

5. **`mouseup`** 이 진행될때 **`isPainting = true`** 되서 if문의 거짓 부분을 실행해 
   마우스가 움직이는 위치를 시작점으로 바꾼다. 


# 오류발생 

그림을 그리는 중에 **`mousedowm`** 을 유지한채 그림판 밖을 나갔다 들어온후에     
**`mouseup`** 이 됐음에도 불구하고 마우스를 움직이는 것만으로도 그림을 그릴 수 있다. 

# 오류 해결 


```js
canvas.addEventListener("mouseleave",cancelPainting); 
```

오류를 해결하기위해 위의 코드를 추가해주자. 이제 마우스가 그림판 밖을 벗어날때도    
**`cacelPainting`** 함수가 실행돼 오류가 해결되는걸 확인할 수 있을 것이다. 

```toc

```