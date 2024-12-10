---
emoji: 👨🏻‍💻
title: Day 17 HTTP, Express.js
date: '2024-12-10 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# HTTP

브라우저와 웹 서버 간의 데이터 통신을 담당하는 프로토콜로 웹에서 데이터를 요청(Request)하고
응답(Response)받는 데 사용이 됩니다. HTTP는 클라이언트(예: 브라우저)와 서버 간의 요청-응답 모델을
기반으로 작동하며, 주로 HTML, CSS, JavaScript, 이미지, 동영상 등의 리소스를 주고받을 때 활용된다고 합니다.

## HTTP 특징

1. 클라이언트-서버 구조

- HTTP는 클라이언트(예: 웹 브라우저)와 서버 간의 요청(Request)과 응답(Response)으로 이루어진 통신 프로토콜 클라이언트가 요청을 보내면, 서버는 해당 요청에 대한 응답을 반환합니다.

2. Stateless(상태 비저장성)

- HTTP는 각 요청 간의 상태를 저장하지 않습니다. 즉, 하나의 요청이 끝나면 이전 요청의 정보를 기억하지 않는 특징
  이를 보완하기 위해 쿠키, 세션, 토큰(JWT) 같은 기술이 같이 활용됩니다.

3. 텍스트 기반 프로토콜

- HTTP 메시지는 사람이 읽을 수 있는 텍스트 형식으로 작성됩니다.
- 요청 메시지: GET /index.html HTTP/1.1
- 응답 메시지: HTTP/1.1 200 OK

4. 캐시(Cache) 지원

- HTTP는 서버와 클라이언트가 캐싱을 통해 데이터를 임시 저장하여 네트워크 요청을 줄이고 성능을 향상시킵니다.
- 주요 캐시 제어 헤더: Cache-Control, Expires, ETag

# Express.js

Express.js는 Node.js 환경에서 실행되는 웹 애플리케이션 프레임워크로, 빠르고 간결하며 유연한 서버
개발을 가능하게 합니다. Express는 Node.js의 기본 HTTP 모듈 위에 구축되어 웹 애플리케이션과 API를
효율적으로 만들 수 있는 다양한 기능을 제공합니다.

=> Node.js 다양한 웹 프레임워크가 존재하지만 SSR(정적 웹페이지 렌덩링)의 경우 Express를 가장 선호합니다.

## Express.js 특징

1. 경량 프레임워크

- Express는 최소한의 기능만 포함하여 작고 빠릅니다.
- 필요한 기능은 미들웨어를 통해 추가할 수 있습니다.
- 미들웨어: Express.js에서 요청(Request)과 응답(Response) 사이의 처리를 담당하는 함수입니다.

2. 미들웨어 기반 구조

- 요청과 응답을 처리하기 위한 로직을 단계별로 추가할 수 있는 미들웨어 시스템을 제공합니다.
- 예: 로깅, 인증, 오류 처리 등

3. 라우팅 시스템

- URL 경로와 HTTP 메서드에 따라 요청을 처리하는 강력한 라우팅 기능을 지원합니다.
- 동적 경로 매칭, 쿼리 매개변수 처리 등을 제공

4. 템플릿 엔진 지원

- 다양한 템플릿 엔진(EJS, e.g., Pug)과 통합하여 동적 HTML 페이지를 생성합니다.

5. 유연성과 확장성

- 다양한 플러그인과 라이브러리를 쉽게 통합하여 기능을 확장 가능 합니다.
- RESTful API, GraphQL 등 다양한 스타일의 서버 구축 가능 합니다.

## 간단한 Express 예제

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
app.use(express.urlencoded());

// get방식 처리하는 방법
// https://expressjs.com/en/4x/api.html#app.get
// path 3가지 패턴이 올수 있다. '/'=root, ['/', '/index', '/home'], '^home*[0-9]*$'=정규식 도 가능
app.get(['/', '/index', '/home'], (req, res) => {
  res.status(200);
  res.render('home');
  // res.render( __dirname + '/views' + 'home'); // 이건 안돌아간다.
});

app.listen(port, () => {
  console.log(`Listening on http://127.0.0.1:${port}`);
});
```

### 1. 주요 모듈 및 포트 설정

```js
const express = require('express'); // Express.js 모듈 로드
const app = express(); // Express 애플리케이션 생성
const port = 3000; // 서버가 사용할 포트 설정
```

- express: Node.js에서 웹 서버를 쉽게 구축할 수 있도록 도와주는 프레임워크입니다.
- app: Express 애플리케이션 객체입니다. 이를 통해 서버 설정, 라우팅, 미들웨어 추가 등을 수행합니다.
- port: 서버가 실행될 포트 번호를 지정합니다. 여기서 3000번 포트를 사용하도록 설정되어 있습니다.

### 2. 정적 파일 제공

```js
app.use(express.static('public'));
```

- express.static('public'): public 폴더를 정적 파일 제공 디렉토리로 설정합니다.
  - 예: public 폴더에 css/style.css라는 파일이 있다면, 클라이언트가 /css/style.css URL로 접근할 수 있습니다.
- 정적 파일: HTML, CSS, 이미지, JS 등과 같은 변경되지 않는 리소스.

### 3. 템플릿 엔진 설정

```js
app.set('view engine', 'ejs');
app.set('views', __dirname + '/views');
```

- 템플릿 엔진: 서버에서 HTML 파일을 동적으로 생성하는 데 사용됩니다.
- 여기서는 EJS (Embedded JavaScript Templates)를 사용합니다.
- view engine: 렌더링에 사용할 템플릿 엔진을 설정합니다.
- views: EJS 파일이 저장된 폴더의 경로를 설정합니다. 기본적으로 views 폴더를 사용합니다.

### 4. JSON 및 URL-encoded 데이터 처리

```js
app.use(express.json());
app.use(express.urlencoded());
```

- express.json(): JSON 데이터를 파싱하도록 설정합니다. 클라이언트가 JSON 데이터를 요청 본문(body)에 포함하여 보내면 이를 해석합니다.
- express.urlencoded(): URL-encoded 데이터를 처리하도록 설정합니다. 예를 들어, HTML 폼 데이터(POST 방식)를 처리할 수 있습니다.

### 5. GET 라우팅

```js
app.get(['/', '/index', '/home'], (req, res) => {
  res.status(200);
  res.render('home');
});
```

- app.get(): HTTP GET 요청을 처리하는 라우트를 정의합니다.
- 라우트 패턴:
  - / : 루트 경로
  - /index 및 /home : 이 경로들도 동일하게 처리됩니다.
- res.status(200): 응답 상태 코드를 200으로 설정(정상 처리).
- res.render('home'): views/home.ejs 파일을 렌더링하여 클라이언트에 응답합니다.

### 6. 서버 실행

```js
app.listen(port, () => {
  console.log(`Listening on http://127.0.0.1:${port}`);
});
```

- app.listen(): 서버를 지정된 포트에서 실행합니다.
- console.log: 서버가 실행되면 해당 메시지가 콘솔에 출력됩니다.

```toc

```
