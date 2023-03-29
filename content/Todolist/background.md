---
emoji: 🧢
title: TodoList (4)  - 배경화면 바꾸기 기능 구현
date: '2023-03-28 15:00:00'
author: Js 
tags: TodoList 작성 
categories: TodoList Js 
---
# 배경화면 바꾸기 기능 구현 

## 소스코드 


```js
const images = ["1.jpg", "2.jpg", "3.jpg","4.jpg","5.jpg"];
const bgImage = document.createElement("img"); //img 태그 생성 
const changeBtn = document.querySelector(".changeBackgroud");
changeBtn.addEventListener("click", changeBackgroud);
const chosenImage = images[Math.floor(Math.random() * images.length)];
bgImage.src = `img/${chosenImage}`;
document.body.appendChild(bgImage);

function changeBackgroud() {
    const chosenImage = images[Math.floor(Math.random() * images.length)];
    /*
    Math.floor 반올림, Math.random -> 0~1 범위 내에서 무작위 난수를 발생
    암호학적으로 안전한 난수를 발생시키지 않아 보안과 관련해서는 사용하지 말아야 한다 
    그 대신 Web Crypto API의 window.crypto.getRandomValues() 메소드를 이용하여야 한다.
    */
    bgImage.src = `img/${chosenImage}`; //img의 src를 생성
    document.body.appendChild(bgImage); //bdImage를 body에 자식 요소로 추가한다 

}

```
<br>
<br>

# 배경이미지 랜덤 생성

```js
const images = ["1.jpg", "2.jpg", "3.jpg","4.jpg","5.jpg"];
const bgImage = document.createElement("img");
const changeBtn = document.querySelector(".changeBackgroud");
changeBtn.addEventListener("click", changeBackgroud);
const chosenImage = images[Math.floor(Math.random() * images.length)];
bgImage.src = `img/${chosenImage}`;
document.body.appendChild(bgImage);
```

1. 이미지 태그를 생성하기 위해 **document.createElement("img")** 를 사용함   
     
    + createElement()에 생성하고자 하는 태그를 입력 
   
2. **const chosenImage = images[Math.floor(Math.random() * images.length)]**   

    + 배경 선택을 랜덤으로 하기 위해서 0~1사이에 난수를 생성는 **Math.random**을 사용   

    + 발생한 난수를 images 배열의 길이 만큼 곱해 0 ~ images.length 사이에 난수를 생성   

    + Math.floor를 사용해 소수점 뒷자리를 반올림해 정수를 생성   

    + 암호학적으로 안전한 난수를 발생시키지 않아 보안과 관련해서는 사용하지   
       말아야 한다 그 대신 Web Crypto API의 window.crypto.getRandomValues()   
       메소드를 이용하여야 한다.   
   
3. **bgImage.src = img/${chosenImage}**     
   
    + 생성된 img태그의 src를 지정
     
4. **document.body.appendChild(bgImage)**    
     
     + createElement("img")와 bgImage.src = **img/${chosenImage}** 를 사용해 생성된      
     `img src = "chosenImage` 가  body의 자식으로 들어간다 
