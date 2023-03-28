#  HTML구조 작성 

## 소스코드 


```html
<body>
    <main>
        <div class="main-left">
            <div class="login">
                <form  id ="login-form" class="hidden"> 
                    <input id="name" type="text" placeholder="이름을 적어주세요">
                    <input id="submit" type="submit" value="login">
                </form>
                <h1 class="hidden" id="greeting">1</h1>
                <div class="music">
                    <div class="music-option">music</div>
                    <div class="music-controll">
                        <button class="music-btn on">On</button>
                        <button class="music-btn pause">Pause</button>
                        <button class="music-btn off">Off</button>
                    </div>
                </div>
                <div class="volume">
                    <div>volume</div>
                        <input class="volume-controll" type="range" step="0.01"
                        min="0" max="1" value="0.5">
                </div>
                <div class="backGround">
                    <button class="changeBackgroud">배경바꾸기</button>
                </div>
            </div>
            <div class="clock">
                <span id="day"></span>
                <span id="time"></span>
                <span id="weather"></span>
            </div>
            <div class="calendar">
                <div class="header">
                    <div class="year-month"></div>
                    <div class="nav">
                        <button class="nav-btn go-pre">&lt;</button>
                        <button class="nav-btn go-today">Today</button>
                        <button class="nav-btn go-next">&gt;</button>
                    </div>
                </div>
                <div class="main">
                    <div class="days">
                        <div class="day">일</div>
                        <div class="day">월</div>
                        <div class="day">화</div>
                        <div class="day">수</div>
                        <div class="day">목</div>
                        <div class="day">금</div>
                        <div class="day">토</div>
                    </div>

                </div>
                <div class="dates"></div>
            </div>
        </div>
        <div class="main-right">
            <div class="todo-box">
                <form class="todo">
                    <input id="todos" type="text" placeholder="일정을 적어주세요" required>
                </form>
                <ul id="todo-list"></ul>
            </div>
            <div class="qoute-box">
                <div class="quote-box-box">
                    <div class="first">Today Qoute</div>
                    <div></div>
                    <div></div>
                </div>
            </div>
        </div>
    </main>
</body>

```

## login 


```html
<div class="login">
    <form class="login_form">
    <input id="name" type="text" placeholder="이름을 적어주세요">
    <input id="submit" type="submit" value="login">
    </form>
    <h1 class="greeting" id="hidden"></h1>
    
    <div class="music">
    <div class="music-option">music</div>
    <div class="music-controll">
        <button class="music-btn on">On</button>
        <button class="music-btn pause">Pause</button>
        <button class="music-btn off">Off</button>
    </div>
    </div>
    <div class="volume">
        <div>volume</div>
        <input class="volume-controll" type="range" step="0.1"
            min="1" max="10" value="0.5">
    </div>
    <div class="backGround">
        <button class="changeBackgroud">배경바꾸기</button>
    </div>
</div>
```

## login_form 

**input의 유효성을 검사하기 위해서 form 태그를 사용**

## clock 


```html
 <div class="clock">
    <span id="day"></span>
    <span id="time"></span>
    <span id="weather"></span>
</div>
```

## calendar   


```html
<div class="calendar">
    <div class="header">
    <div class="year-month"></div>
    <div class="nav">
        <button class="nav-btn go-pre">&lt;</button>
        <button class="nav-btn go-today">Today</button>
        <button class="nav-btn go-next">&gt;</button>
    </div>
</div>
    <div class="main">
        <div class="days">
            <div class="day">일</div>
            <div class="day">월</div>
            <div class="day">화</div>
            <div class="day">수</div>
            <div class="day">목</div>
            <div class="day">금</div>
            <div class="day">토</div>
        </div>
    </div>
    <div class="dates"></div>
</div>
```

## dates  

**js로 날짜를 대입하기 위해서 만들어 둠**

<br>
<br>

# style.css 기본구조 작성 


```css
@import "css/login.css";
@import "css/music.css";
@import "css/volume.css";
@import "css/backGround.css";
@import "css/clock.css";
@import "css/calendar.css";
@import "css/todo.css";
@import "css/quote.css";

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box; // 설명 추가 
}

body {
    margin: 0;
    padding: 0;
    height: 100vh;
    width: 100vw;
    border: 1px solid gray;
    display: flex;
    justify-content: center;
    align-items: center;

}

main {
    width: 1000px;
    height: 900px;
    border: 1px solid gray;
    display: flex;
}

.main-left {
    display: flex;
    flex-direction: column;
    align-items: center
}

.main-right {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
```

[box-sizing 에 대한 설명](https://www.codingfactory.net/10630)

1. **box-sizing: border-box** 


2. **`body`** 높이는 100vh를 너비는 100vw를 할당   
    + **`100vh`** -  **`100vh`** 는 부모 태그와는 상관없이 보이는 Viewport Height의 100%를<br>
          다 쓰겠다는 의미입니다.    
    + **`100vvw`** - **`100vh`** 는 부모 태그와는 상관없이 보이는 Viewport width의 100%를<br>
          다 쓰겠다는 의미입니다. 


3. 테두리된 영역을 좌우, 상하 가운데 정렬하기 위해 **`display`** 를 적용하고   
   **`justify-content: center`** 와 **`align-items: center`** 사용


4. main의 영역을 보면 **`main-left`** 와 **`main-right`** 두개의 역역을 나눠진다. 


5. **`main-left`** 와 **`main-right`** 영역을 보면 **`item`** 의 축이 column로 되어있다. 
   **`display`**  를 적용하고 **`flex-direction: column`** 를 사용해 **`flex`** 축을 **`column`** 으로 설정 

6. body의 영역과 마찬가지로 **좌우,상하 가운데 정렬을** 해준다 


## login.css 


```css
.login {
    width: 547px;
    height: 170px;
    margin: 20px;
    padding: 15px;
    display: flex;
    flex-direction: column;
    border: 1px solid gray;
    border-radius: 10px;
    justify-content: center;
    align-items: center;

.hidden {
    display: none;
}

#login-form {
    /* display: flex; */
    margin-bottom: 10px;
}

#login-form input {
    font-size: 20px;
    padding: 10px;
    border-radius: 15px;
}

#login-form input:focus {
    outline: none;
}

#login-form input::placeholder {
    color: black;
}
```

## music.css


```css
.music {
    display: flex;
    align-items: center;
    margin-bottom: 5px;
}

.music-option {
    margin-right: 10px;
}

.music-controll {
    padding: 0px 5px;
}

.music-btn {
    border-radius: 10px;
    padding: 3px;
}

```

## volume.css 


```css
.volume {
    display: flex;
    align-items: center;
    margin-bottom: 5px;
}

.volume div {
    margin-right: 10px;
}

.volume input[type="range"] {
    border: 1px solid black;
    background-color: transparent;
    border-radius: 10px;
}
```

## clock.css 


```js
/* 시계 */
.clock {
    width: 547px;
    height: 170px;
    margin: 20px;
    padding: 15px;
    border: 1px solid gray;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

#day {
    font-size: 20px;
    color: black;
    font-weight: bold;
}

#time {
    font-size: 50px;
    font-weight: bold;
}

#weather {
    font-size: 20px;
    font-weight: bold;
}
```

## calendar.css 


```css
.calendar {
    width: 547px;
    height: 450px;
    margin: 20px;
    padding: 15px;
    border: 1px solid gray;
    border-radius: 10px;
}
```

 **캘린더에 자세한 내용은 기능 구현을 할때 설명하겠습니다.** 

## todo.css 


```css
.todo-box {  
    width: 373px;
    height: 580px;
    margin: 20px;
    padding-bottom: 40px;
    border: 1px solid gray;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.todo {
    width: 306px;
    height: 50px;
}

.todo input{
    width: 276px;
    padding: 10px;
    border-radius: 15px;
}

#todo-list {
    width: 373px;
    height: 390px;
    overflow-x: none;
    overflow-y: scroll;
    word-break: break-all;
    font-weight: bold;
    font-size: 20px;
 
}

#todo-list li{
    display: flex;
    justify-content: space-around;
    padding: 10px;
    margin: 5px;
}
```

1. **`overflow-x: none`** , **`overflow-y: scroll`**   
   -> 리스트 내용이 많을때 이용 y축 scroll만 존재   


2. **`word-break: break-all`**    
   -> 텍스트가 범위 밖으로 나갈때 자동으로 줄 바꿈 


3. #todo-list li에서 **`display`** 를 이용한 것은 리스트의    
   내용과 delete 아이콘을 **`flex`** 하기 위함이다 

## quote.css 


```css
.qoute-box {
    width: 373px;
    height: 250px;
    margin: 20px;
    border: 1px solid gray;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.qoute-box-box {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
}
```
