---
emoji: 🧢
title: TodoList (5) - 날씨 정보 가져오기
date: '2023-03-28 16:00:00'
author: Js 
tags: TodoList 작성 
categories: TodoList Js 
---
# API를 이용해 날씨 정보 가져오기 

## 소스코드 


```js
const weather = document.querySelector("#weather");
const API_KEY = "4dd7add724570dbc3c2270897dd5257b";

function onGeoOk(position) {
    const lat = position.coords.latitude;
    const lon = position.coords.longitude;
    const url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`;
    fetch(url)
        .then((response) => response.json())
        .then((data) => {
            weather.innerText = `${data.name} / ${data.weather[0].main} / ${data.main.temp} `;
        });
}

function onGeoError() {
    alert("Can't find you. No weather for you.");
}
navigator.geolocation.getCurrentPosition(onGeoOk, onGeoError);
// 장치의 현재 위치를 가져옴, 위치를 얻는데 성공지 onGeok 실행 실패시 onGeoError 실행  
```

1. **`navigator.geolocation.getCurrentPosition(onGeoOk, onGeoError)`** 

     + 장치의 현재 위치를 가져오게 됩니다 

     + 위치를 얻는데 성공하면 **onGeok()** 함수를 실행하고 실패시   
        **onGeoError()** 함수를 실행 
<br>
<br>

## API 이용 

1. google에 openWeather -> API -> Current weather data에 접속

2. 로그인 진행 후 영문이름을 클릭하게 되면 MY API KEYS를 통해서 Key값을 확인 

<br>
<br>

## onGeoOk 함수 

1. **onGeoOk()** 함수의 인자는 **GeolocationPosition** 객체를 가져온다 

2. **GeolocationPosition** 객체의 **position.coords** 부분을 보게 되면   
   위도와 경도를 확인할 수 있다 

3. API 호출 예시를 보게 되면 **https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}** 되어 있다 

4. &units=metric 부분을 추가하게 되면 섭씨로된 온도를 확인할 수 있다 

5. **fetch(url)**    

    + 반환받은 요청 (response)은 then 메서드 콜백인자로 들어가게 된다.    

6. **.then((response) => response.json())**   
  
    + response의 json() 메서드를 호출한다.   
  
    + 응답내용을 json으로 변환한 다음 then의 콜백인자로 넘겨준다.   

7. **.then((data) =>**    
  
    + 넘겨받은 값을 통해 필요한 정보를 추출한다. 


<br>
<br>

## onGeoError 함수 

1. 장치의 현재 위치를 가져오는데 실패시 **onGeoError** 함수 실행 

2. Can't find you. No weather for you. 라는 메시지의 경고창이 뜸 
