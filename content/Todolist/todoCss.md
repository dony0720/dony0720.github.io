---
emoji: 🧢
title: TodoList (11) - style.css 마무리 
date: '2023-03-29 16:50:00'
author: 중석 
tags: TodoList 작성 
categories: Js CSS
---
# style 마무리 

## 소스코드 

## login.css 


```css
.login {
    background-color: rgba(0, 0, 0, 0.1);
    /*(red, green, blue, opacity)*/
    transition: all 0.5s ease-in-out;
}

#login-form {
    display: flex; 
}


#login-form input {
    background: transparent; // 배경색을 투명하게 지정 
    box-shadow: 0px 0px 2px 0px rgba(0, 0, 0, 0.5);
}


```

1. **`background-color: rgba(0, 0, 0, 0.1)`** 
      red, blue, green, opcity 순으로 값을 주어 배경 색 지정 

2. **`background: transparent`**
      배경색을 투명하게 지정 



## music.css 


```css
.music {
    font-weight: bold;
}

.music-btn {
    background-color: transparent; 
    font-weight: bold;
}
```

## volume.css 


```css
.volume input[type="range"] {
    -webkit-appearance: none; 
}
```

1. `-webkit-appearance: none` 또는 `appearance: none` 속성을 통해 
    기본 CSS 스타일을 사용하지 않겠다고 선언해야만 위와 같은 CSS 스타일링을 반영할 수 있습니다. 
    그렇지 않으면 맨 기본적인 `range slider` 처럼 보이게 됩니다.

## clock.css 


```css
.clock {
    background-color: rgba(0, 0, 0, 0.1);
}

```

## todo.css 


```css
.todo-box {
    background-color: rgba(0, 0, 0, 0.1);
}

.todo input{
    background-color: transparent;
}

```

## backGround.css


```css
.changeBackgroud{
    background-color: transparent;
    border-radius: 10px;
    font-weight: bold;
    padding: 3px;
}

/* 배경 */
img {
    position: absolute;
    width: 100vw;
    height: 100vh;
    left: 0px;
    top: 0px;
    right: 0px;
    bottom: 0px;
    z-index: -1;
    /* 우선순위를 낮춰서 이미지를 가장 뒤로 가게 함*/
    background-size: cover;
}
```

## quote.css
```css
.quote-box {
    width: 373px;
    height: 250px;
    margin: 20px;
    border: 1px solid gray;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: rgba(0,0, 0, 0.1);
    cursor: pointer;
}

.quote-box div:nth-child(1){
    font-weight: bold;
    font-size: 18px;
}
```

```toc

```