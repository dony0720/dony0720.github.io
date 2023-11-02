---
emoji: 🖋
title: Canvas (3) 
date: '2023-03-30 16:50:00'
author: Js 
tags: Canvas를 이용한 그림판
categories: Js 
---
# Fill, Draw 모드 

## HTML - Fill, Draw 모드 


```html
<button id = "mode-btn">Fill</button>
```

# app.js 


```js
const modeBtn = document.querySelector("#mode-btn");
let isFilling = false;

function btnMode() {
  if (isFilling) {
    isFilling = false;
    modeBtn.innerText = "Draw";
  }
  else {
    isFilling = true;
    modeBtn.innerText = "Fill";
  }
}

function FillDraw(){
  if (isFilling){
      ctx.fillRect(0, 0, 800, 800)
    }
 }

modeBtn.addEventListener("click", btnMode);
canvas.addEventListener("click",FillDraw)
```

# btnMode() 함수 

1. 먼저 Fill 모드와 Draw 모드를 한 버튼 안에서 실행하기 위해서 버튼의 텍스트를 바꾸는 작업을 해야한다. 
    
2. `isFilling` 변수를 선언하고 `false` 를 할당한다. 
    
3. 버튼을 클릭할때 Fill -> Draw로 바껴야 하기 때문에 함수의 `false`부분에 `mode.innerText = "Fill"` 을 할당하고   
   `isFilling` 을 `true` 로 바꾸어 줘야 동적인 함수가 된다. 
       
4. 코드를 실행해보면 버튼을 클릭할때마다 글씨가 바뀌는걸 볼 수 있을 것이다. 

# FrillDraw() 함수 

1. `isFilling = true` 일 때는 버튼의 글씨가 `Fill`인 상태이다.    
   그래서 우리는 이 때 그림판을 클릭했을때 지정된 색으로 그림판을 채워주면 된다. 
   
2. if문을 사용해서 `isFilling = true` 일때 ctx.fillRect(0, 0, 800, 800)를 사용해 그림판을 채운다 

# Erase, Reset 모드 

## HTML - Erase, Reset 모드 


```html
<button id = "Erase-btn">Erase</button>
```

# app.js 


```js
const erase = document.querySelector("#Erase-btn");
let isErasing = false;

const reset = document.querySelector("#Reset-btn");

function Erase(){
  ctx.strokeStyle = "white";
  isFilling = false;
  modeBtn.innerText = "Draw";
}

function Reset(){
  ctx.fillStyle = "white";
  ctx.fillRect(0, 0, 800, 800);
}

erase.addEventListener("click", Erase)
reset.addEventListener("click", Reset)
```

1. **Erase 모드**는 그림판을 하얀색 선으로 **Draw모드**를 하는 것과 같다. 

    + ctx.strokeStyle = "white" 사용해 선의 색상을 하얀색으로 지정한다. 
    
    + Draw 모드를 하기위해 isFilling = false로 할당한다. 
    
    + Draw 모드 일때는 버튼의 글씨가 "Draw" 로 지정해주어야 하기 때문에 modeBtn.innerText = "Draw" 사용해서 글씨를 바꿔준다. 
    
    
2. **Reset 모드**는 그림판을 하얀색 도형으로 **Fill 모드**를 하는 것과 같다. 
    
    + ctx.fillStyle = "white" 사용해서 도형을 채우는 색상을 하얀색으로 지정한다.
    
    + ctx.fillRect(0, 0, 800, 800) 사용해 800x800의 그림판을 채운다. 

```toc

```