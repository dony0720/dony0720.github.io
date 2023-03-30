---
emoji: 🧢
title: TodoList (3) - MP3 기능 구현
date: '2023-03-28 15:00:00'
author: Js 
tags: TodoList 작성 
categories: TodoList Js 
---
# mp3 player 기능 

## 소스코드 


```js
const mp3 = new Audio("bird.mp3")
const soundBtn = document.querySelector(".volume-controll");
const onBtn = document.querySelector(".on")
const pauseBtn = document.querySelector(".pause")
const offBtn = document.querySelector(".off")

function play() {
    mp3.loop = true;
    mp3.volume = soundBtn.value / 10;
    mp3.play();
}

function pause() {
    mp3.pause();

}

function stop() {
    mp3.pause();
    mp3.currentTime = 0;
}
onBtn.addEventListener("click", play)
pauseBtn.addEventListener("click", pause)
offBtn.addEventListener("click", stop)
```

## play 함수 


```js
function play() {
    mp3.loop = true;
    mp3.volume = soundBtn.value / 10;
    mp3.play();
}
```

1. **mp3.loop = true :**   
    + 오디오를 반복 재생함 
<br>
<br>

2. **mp3.volume = soundBtn.value**   
    + 음량은 0.0 ~ 1.0 사이 값으로 지정할 수 있고, 1.0이 가장 큰 음량

<br>
<br>

## 자주 쓰이는 Audio 객체의 속성

1. **`audio.autoplay = true`**
    
    + audio가 load 될 때 자동재생됨
<br>
<br>

2. **`audio.currentTime = 5`**
    
    + audio의 재생시점을 5초로 설정함
<br>
<br>

3. **`audio.duration`**

    + audio의 길이를 초(seconds) 단위로 반환
<br>
<br>

4. **`audio.loop = true`**

    + audio를 반복 재생함
<br>
<br>

5. **`audio.src = "my_audio.mp3"`**

    + audio의 경로를 지정함(URL)
<br>
<br>

6. **`audio.volume = 0.2`**

    + audio의 음량을 0.2로 지정함
      음량은 0.0 ~ 1.0 사이 값으로 지정할 수 있고, 1.0이 가장 큰 음량

<br>
<br>

## 자주 쓰이는 Audio 객체의 메소드

1. **`audio.play()`**

    + 오디오를 재생시킴 
<br>
<br>

2. **`audio.pause()`**

    + 오디오를 일시정지함 
<br>
<br>

3. **`audio.load()`**

    + audio를 다시 load함
      주로 audio의 src나 설정이 바뀌었을 경우에 사용


```toc

```