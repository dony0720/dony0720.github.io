---
emoji: 👨🏻‍💻
title: Day 18 router 모듈화, 레이아웃 모듈화
date: '2024-12-11 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# Node.js route

## 외부 선언 router 적용 (app.js)

```js
const express = require('express');
const app = express();
const port = 3000; // 포트 번호 설정, 0 ~ 65555, 0 ~ 1023 = 사용하지 말것 웬만하면!!

// 정적파일(static)라우팅을 위한 static 폴더 지정
// /css/style.css
app.use(express.static('public'));

// 템플릿 엔진 활용을 위한 ejs 미들웨어 등록
app.set('view engine', 'ejs');

// views 폴더를 기본 템플릿(ejs파일) 폴더로 등록
app.set('views', __dirname + '/views');

// json 파라미터 처리를 위해 적용
app.use(express.json());

// post(post x-www-form-urlencoded) 처리를 적용
app.use(express.urlencoded({ extended: true }));

// get방식 처리하는 방법
app.get(['/', '/index', '/home'], (req, res) => {
  res.status(200);
  res.render('home');
});

// 외부에서 선언한 라우터(handler)를 적용하는 방법
app.use('/', require('./routes/getPage'));

app.listen(port, () => {
  console.log(`Listening on http://127.0.0.1:${port}`);
});
```

- app.use( '/', ... )는 기본 경로( / )로 들어오는 모든 요청에 대해 미들웨어를 실행합니다.
- require( './routes/getPage' )는 애플리케이션이 사용할 라우트를 정의한 파일을 가져옵니다.

## router 모듈화 (getPage.js)

```js
// 사용할 모듈 import
const express = require('express');
const asyncHandler = require('express-async-handler');
const router = express.Router();
const bcrypt = require('bcrypt');

// get page 요청 가져오기
router.get('/getPage', (req, res) => {
  res.status(200).render('getPage');
});

// express-async-handler 기반으로 비동기 처리하는 방법

const registerMember = asyncHandler(async (req, res) => {
  const member = req.query;

  // password 암호화
  const hashedPassword = await bcrypt.hash(member.pw, 10);
  member.pw = hashedPassword;

  res.send('req : ' + req.query.toString());

  // 렌더링 하는 방법
  res.render('result.ejs', { member });
});

router.route('/get_result').get(registerMember).post(registerMember);

module.exports = router;
```

### 1. 사용된 모듈

```js
const express = require('express');
const asyncHandler = require('express-async-handler');
const router = express.Router();
const bcrypt = require('bcrypt');
```

- express-async-handler: 비동기 함수에서 발생하는 예외를 자동으로 처리하여 next()로 전달합니다. 이를 통해 try-catch를 명시적으로 작성할 필요가 줄어듭니다.
- router: Express에서 제공하는 라우터 객체로, 경로별로 요청을 처리할 수 있습니다.
- bcrypt: 암호화를 위한 라이브러리로, 비밀번호를 해시(hash) 처리하거나 비교하는 데 사용됩니다.

### 2. GET 요청 처리

```js
router.get('/getPage', (req, res) => {
  res.status(200).render('getPage');
});
```

- /getPage 경로로 들어오는 GET 요청을 처리합니다.
- res.status(200).render('getPage') : 반드시 요청이 성공된 후에 getPage라는 이름의 템플릿(예: EJS 파일)을 렌더링합니다.

### 3. 비동기 요청 처리 (registerMember)

```js
const registerMember = asyncHandler(async (req, res) => {
  const member = req.query;

  // password 암호화
  const hashedPassword = await bcrypt.hash(member.pw, 10);
  member.pw = hashedPassword;

  res.send('req : ' + req.query.toString());

  // 렌더링 하는 방법
  res.render('result.ejs', { member });
});
```

1. 비동기 핸들링

   - **asyncHandler**로 감싸 비동기 작업 중 발생할 수 있는 오류를 처리합니다.
   - 예를 들어, bcrypt.hash에서 에러가 발생해도 서버가 멈추지 않고 에러를 Express의 기본 에러 처리기로 넘깁니다.

2. 입력 데이터 가져오기

   - req.query: 클라이언트가 URL 쿼리 문자열로 보낸 데이터를 가져옵니다.

3. 비밀번호 암호화

- bcrypt.hash(member.pw, 10): 입력받은 비밀번호(member.pw)를 10번의 salt 작업을 거쳐 암호화합니다.
- 결과는 hashedPassword에 저장되고, member.pw 값을 암호화된 비밀번호로 업데이트합니다.

4. 응답

- res.send(): 단순히 문자열을 응답.
- res.render(): result.ejs 템플릿 파일을 렌더링하고, member 데이터를 전달.

### 4. 라우트 설정

```js
router.route('/get_result').get(registerMember).post(registerMember);
```

- /get_result 경로에 대해 GET과 POST 요청을 모두 registerMember 함수로 처리합니다.

# 모듈화된 레아아웃 적용

## app.js

```js
const express = require('express');
const port = 3000;

const app = express();

// 정적파일(static) 라우팅을 위해 static 폴더 지정
app.use(express.static('public'));
// 템플릿 엔진 활용을 위해 ejs 적용
app.set('view engine', 'ejs');
// views 폴더를 기본 템플릿 폴더로
app.set('views', __dirname + '/views');
// json 파라미터 처리를 위해 적용
app.use(express.json());
// post(post x-www-form-urlencoded) 처리를 적용
app.use(express.urlencoded());

// .js 확장자 생략 가능
app.use('/', require('./routes/index'));
app.use('/', require('./routes/practice1'));
app.use('/', require('./routes/practice2'));

app.listen(port, () => {
  console.log(`Listening on http://127.0.0.1:${port}`);
});
```

## 레이아웃 모듈화

### header.ejs

```js
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Blog</title>
  <meta name="description" content="My first application using Node.js, Express and MongoDB">
  <link rel="stylesheet" href="/css/style.css">
</head>
<body>

  <div class="container">

    <!-- 헤더 : 로고, 상단 메뉴, 로그인 -->
    <header class="header">
      <!-- 로고 -->
      <a href="/" class="header-logo"><img src="/img/programmers-logo-dark.png" alt="" width="100px"></a>

      <!-- 상단 메뉴 -->
      <nav class="header-nav">
        <ul>
          <li>
            <a href="#">Home</a>
          </li>
          <li>
            <a href="#">About</a>
          </li>
        </ul>
      </nav>

      <!-- 관리자 로그인 -->
      <div class="header-button">
        <a href="#">관리자 로그인</a>
      </div>
    </header>
```

- header 닫는 태그의 윗부분만 코드를 작성합니다.

```js
<footer>
  <nav>
      <a href='https://programmers.co.kr/' target='_blank'>프로그래머스</a>
      <a href='https://github.com/' target='_blank'>Github</a>
  </nav>
  <p>
      <span>Copyright 2024. programmers. All Rights Reserved.</span>
      <span>서울시 강남구 역삼동</span>
      <span>02-1234-5678</span>
  </p>
</footer>

</body>


</html>
```

footer 태그부터 html 닫는 태그까지 작성합니다. 이후 다른 ejs 파일에서 header.ejs와 footer.ejs 파일을 합쳐 하나의 페이지를 구성하게 됩니다.

## 레이아웃 모듈 include (index.ejs)

```html
<!-- include header -->
<%-include('./header.ejs')%>

<div class="container">
  <!-- 상단 소개글, 히어로 이미지 -->
  <div class="top">
    <h1 class="top-heading">연습용 페이지</h1>
    <a href="/home">1. Home</a><br />
    <a href="/practice1">2. 문법 연습하기</a><br />
    <a href="/practice2">3. 제어문 연습하기</a><br />
  </div>
  <img
    src="/img/top-hero.jpg"
    alt="노트에 기록하는 모습"
    class="hero-image"
    width="840"
    height="400"
  />
</div>
<!-- include footer -->
<%-include('./footer.ejs')%>
```

<%-include('./header.ejs')%> , <%-include('./footer.ejs')%> 와 같이 작성하게 되면 header와 footer를 index.ejs에서 가져오게 되어 하나의 코드로 렌더링하게 된다.

```toc

```
