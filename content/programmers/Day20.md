---
emoji: 👨🏻‍💻
title: Day 19 fetch 함수
date: '2024-12-13 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# fetch 함수

JavaScript의 fetch 함수는 브라우저 내장 함수로, 네트워크 요청을 보내고 응답을 처리하기 위해 사용됩니다. **HTTP 요청(GET, POST, PUT, DELETE 등)** 을 수행하며, Promise 기반으로 동작하여 비동기적으로 데이터를 처리할 수 있습니다.

## 기본 문법

```js
fetch(url, options)
  .then((response) => {
    /* 응답 처리 */
  })
  .catch((error) => {
    /* 에러 처리 */
  });
```

- url: 요청할 리소스의 URL.
- options: 요청 설정을 담은 객체. 생략하면 기본값으로 GET 요청이 전송됩니다.

## async / await와 함께 사용

### GET 요청

```js
async function getItem() {
  try {
    const id = document.getElementById('input1').value;
    const response = await fetch(`http://localhost:3001/members/${id}`);
    if (!response.ok) {
      throw new Error(response.status);
    }
    const data = await response.json();
    console.log('data:', data);
  } catch (error) {
    console.log(error);
  }
}
```

- fetch API를 사용하여 비동기 POST 요청을 보냅니다.
- URL은 http://localhost:3001/members/로, 로컬 서버를 대상으로 합니다.
- 응답 데이터(response.body)를 JSON으로 파싱하고 data 변수에 저장합니다.

### POST 요청

```js
async function createItem() {
  let id = document.getElementById('inputId').value;
  let name = document.getElementById('inputName').value;
  let age = document.getElementById('inputAge').value;

  const response = await fetch('http://localhost:3001/members/', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ id, name, age }),
  });
  if (!response.ok) {
    throw new Error(response.status);
  }
  const data = await response.json();
  console.log('data:', data);
}
```

- HTTP 요청 헤더에 Content-Type: application/json을 설정해 JSON 데이터로 요청을 보냅니다.
- 요청의 본문(body)에는 사용자가 입력한 데이터를 JSON 형식으로 변환(JSON.stringify)해서 포함시킵니다.
- response.ok가 false라면(즉, HTTP 응답 상태 코드가 200-299 범위를 벗어났다면), 예외를 던져서 에러를 처리합니다.

### PUT 요청

```js
async function updateItem() {
  try {
    let inputId = document.getElementById('inputId2').value;
    let inputName = document.getElementById('inputName2').value;
    let inputAge = document.getElementById('inputAge2').value;

    const response = await fetch(`http://localhost:3001/members/${inputId}`, {
      method: 'PUT',
      body: JSON.stringify({ id: inputId, name: inputName, age: inputAge }),
    });

    if (!response.ok) {
      throw new Error(`에러 발생`);
    }

    const data = await response.json();
    console.log('Updated Item', data);
  } catch (error) {
    console.error('Error:', error);
  }
}
```

- 요청 본문(body)은 JSON 형식으로 변환(JSON.stringify)된 객체입니다.
- 객체에는 업데이트할 id, name, age 값이 포함됩니다.

### DELETE 요청

```js
async function deleteItem() {
  try {
    let inputId = document.getElementById('inputId3').value;

    const response = await fetch(`http://localhost:3001/members/${inputId}`, {
      method: 'DELETE',
    });

    if (!response.ok) {
      throw new Error(`Error: ${response.status}`);
    } else {
      document.getElementById('div4').innerHTML = 'Deleted!!!';
      console.log('Deleted item');
    }
  } catch (error) {
    console.error('Error:', error);
  }
}
```

- fetch를 사용하여 http://localhost:3001/members/{inputId}로 DELETE 요청을 보냅니다.
- method는 DELETE로 설정되어 있습니다. 이는 데이터를 삭제하는 요청임을 서버에 알립니다.

```toc

```
