---
emoji: 🖋
title: Canvas (4) 
date: '2023-03-30 16:50:00'
author: 중석 
tags: Canvas를 이용한 그림판
categories: Js 
---
# 이미지 선택하기 

## Html 


```html
<input type="file" accept="image/*" id ="file">
```

`image` 선택을 할때 비디오 영상인 아닌 image만 선택하기 위해서 `accept="image/*`를 사용했다. 

# app.js 


```js
const file = document.getElementById("file");

function onFileSelect(event){
  const file = event.target.files[0];
  const url = URL.createObjectURL(file); //file을 가리키는 url을 DOMstring으로 반환합니다. 
  const image = new Image(); //image 객체를 생성해 속성들을 추가할 수 있음
  image.src = url; //image 속성 
  image.onload = function(){
  ctx.drawImage(0,0,800,800);
  file.value = null;
  }
  
}
```

# onFileSelect() 함수

1. `const url = URL.createObjectURL(file)` `files`을 가리키는 `url` 을 `DOMstring` 으로 반환한다.

2. `const image = new Image()` image 객체를 생성해 속성들을 추가할 수 있다.

3. `image.onload` 함수 내의 명령은 웹브라우저 내의 모든 요소가 준비된 후 실행이 되도록 힌다..
   
4. `image` 라는 객체가 이미지를 불러온 후에 함수를 실행한다. 

```toc

```