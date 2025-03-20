---
emoji: 📝
title: Axios
date: '2024-03-20 22:00:00'
author: 중석
tags: JS
categories: Js
---

# Axios란?

Axios는 JavaScript에서 HTTP 요청을 쉽게 처리할 수 있도록 도와주는 라이브러리입니다.  
주로 **비동기 통신(AJAX 요청)** 을 수행할 때 사용되며, 브라우저 및 Node.js 환경에서 모두 동작합니다.

## Axios의 특징

1. Promise 기반 : fetch API와 달리, 자동으로 응답을 Promise 객체로 반환하여 then/catch 또는
   async/await 구문을 사용할 수 있습니다.
2. 요청 및 응답 인터셉터 제공 : 요청을 보내기 전이나 응답을 받은 후 , 데이터를 가공할 수 있습니다.
3. 자동 json 변환 : json 데이터를 자동으로 변환하여 편리한 데이터 처리를 지원합니다.
4. 취소 기능 지원 : 요청을 취소할 수 있어 불필요한 API 호출을 막을 수 있습니다.
5. 타임아웃 설정 가능 : 네트워크 지연이 발생할 경우 일정 시간 후 요청을 자동으로 종료할 수 있습니다
6. 브라우저 및 Node.js 지원 : 클라이언트와 서버 환경 모두에서 사용할 수 있습니다.

## 기본 사용법

### GET 요청

```js
// catch - then 구문
axios
  .get('https://jsonplaceholder.typicode.com/posts/1')
  .then((response) => {
    console.log(response.data); // 응답 데이터 출력
  })
  .catch((error) => {
    console.error('오류 발생:', error);
  });

// async - await 구문

async function fetchData() {
  try {
    const response = await axios.get('https://jsonplaceholder.typicode.com/posts/1');
    console.log(response.data);
  } catch (error) {
    console.error('오류 발생:', error);
  }
}
fetchData();
```

### POST 요청

```js
// then - catch 구문
axios
  .post('https://jsonplaceholder.typicode.com/posts', {
    title: 'Axios 테스트',
    body: 'Axios를 이용한 POST 요청',
    userId: 1,
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error('오류 발생:', error);
  });

//  async - await 구문
async function createPost() {
  try {
    const response = await axios.post('https://jsonplaceholder.typicode.com/posts', {
      title: '새로운 게시글',
      body: '이것은 Axios POST 요청을 사용한 예제입니다.',
      userId: 1,
    });

    console.log('응답 데이터:', response.data);
  } catch (error) {
    console.error('오류 발생:', error);
  }
}

createPost();
```

### PUT 요청

```js
// then - catch 구문
axios
  .put('https://jsonplaceholder.typicode.com/posts/1', {
    title: '수정된 제목',
    body: '수정된 내용',
    userId: 1,
  })
  .then((response) => {
    console.log('응답 데이터:', response.data);
  })
  .catch((error) => {
    console.error('오류 발생:', error);
  });

//   async - await 구문
async function editPut() {
  try {
    const response = await axios.put('https://jsonplaceholder.typicode.com/posts', {
      title: '수정한 게시글',
      body: '이것은 Axios PUT 요청을 사용한 예제입니다.',
      userId: 1,
    });

    console.log('응답 데이터:', response.data);
  } catch (error) {
    console.error('오류 발생:', error);
  }
}

editPut();
```

## Axios의 추가 기능

### 요청과 응답 인터셉터

✅ 인터셉터의 종류

1. 요청 인터셉터(Request Interceptor)

- 요청을 보내기 전에 실행됨
- 예: Authorization 토큰 추가, 요청 로깅

2. 응답 인터셉터(Response Interceptor)

- 응답을 받은 후 실행됨
- 예: 응답 데이터 변환, 특정 에러 처리

```js
// 요청 인터셉터
axios.interceptors.request.use(
  function (config) {
    // 요청이 전달되기 전에 실행할 코드
    console.log('요청이 전송되기 전:', config);

    // 모든 요청에 Authorization 헤더 추가 (예: 토큰 기반 인증)
    config.headers.Authorization = 'Bearer sampleToken';

    return config; // 요청을 계속 진행
  },
  function (error) {
    // 요청 오류가 발생했을 때 실행할 코드
    console.error('요청 오류:', error);
    return Promise.reject(error);
  },
);
```

✅ 설명

- axios.interceptors.request.use()를 사용하여 요청 인터셉터를 등록합니다.
- config 객체를 수정하여 모든 요청에 Authorization 헤더를 추가할 수 있습니다.
- 요청을 보내기 전 console.log(config)로 요청 정보를 확인할 수 있습니다.
- 요청에 실패한 경우 Promise.reject(error)를 반환하여 오류를 처리합니다.

```js
// 응답 인터셉터
axios.interceptors.response.use(
  function (response) {
    // 응답 데이터를 가공 (예: 특정 필드만 반환)
    console.log('응답을 받은 후:', response);

    // 예제: 응답 데이터를 직접 가공하여 필요한 값만 반환
    return response.data;
  },
  function (error) {
    // 특정 에러를 처리
    if (error.response) {
      console.error(`오류 발생! 상태 코드: ${error.response.status}`);
    } else {
      console.error('네트워크 오류 또는 응답 없음');
    }

    return Promise.reject(error); // 에러를 계속 전파
  },
);
```

✅ 설명

- 응답을 받은 후 실행되는 함수에서 response.data만 반환하여 필요한 데이터만 추출할 수 있습니다.
- 에러 처리 로직을 추가하여 상태 코드별로 분기 처리할 수도 있습니다.

### 동시 요청 처리

```js
axios
  .all([
    axios.get('https://jsonplaceholder.typicode.com/posts/1'),
    axios.get('https://jsonplaceholder.typicode.com/posts/2'),
  ])
  .then(
    axios.spread((res1, res2) => {
      console.log('첫 번째 응답:', res1.data);
      console.log('두 번째 응답:', res2.data);
    }),
  );
```

### 요청 취소 기능

```js
const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios
  .get('https://jsonplaceholder.typicode.com/posts', {
    cancelToken: source.token,
  })
  .catch(function (thrown) {
    if (axios.isCancel(thrown)) {
      console.log('요청이 취소됨:', thrown.message);
    } else {
      console.error(thrown);
    }
  });

// 특정 상황에서 요청 취소
source.cancel('사용자 요청으로 인해 취소됨.');
```

### 기본 설정 (Base URL & Timeout)

```js
const instance = axios.create({
  baseURL: 'https://jsonplaceholder.typicode.com',
  timeout: 1000, // 1초 타임아웃
  headers: { Authorization: 'Bearer sampleToken' },
});

instance.get('/posts/1').then((response) => console.log(response.data));
```

```toc

```
