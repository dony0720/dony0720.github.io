---
emoji: 👨🏻‍💻
title: Day 16 서버프로그래밍의 개념, Node.js
date: '2024-12-09 22:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 서버 프로그래밍

## 서버사이드 렌더링 (SSR)

서버사이드 렌더링은 이미 완성된 페이지를 브라우저에 제공하는 것이다.

### 동작 방식

1. 브라우저가 서버에 원하는 페이지 요청을 보낸다
2. 서버에서 HTML 페이지를 완전히 생성한 뒤 브라우저로 보낸다.
3. 브라우저는 전달받은 HTML을 그대로 받아 렌더링한다.

### 장점

- 빠른 초기 로딩 시간: 완성된 HTML을 제공하기 때문에, 첫 화면을 로드하는 시간이 빠릅니다.
- 단순한 구조: 클라이언트 측에서 JavaScript 로직이 적어 유지보수가 쉽습니다.

### 단점

- 서버 부하 증가: 모든 요청에서 서버가 HTML을 생성해야 하므로, 트래픽이 많을 경우 서버에 부담이 큽니다.
- 인터랙션 지연: 초기 렌더링은 빠르지만, 페이지 전환 시마다 서버 요청이 필요해 속도가 느려질 수 있습니다.
- 기술적 제한: 실시간 업데이트나 복잡한 사용자 인터페이스를 구현하는 데 불리할 수 있습니다.

즉, 서버사이드 렌더링은 정적인 페이지인 뉴스 콘텐츠, 블로그와 같이 초기 콘텐츠를 빠르게 보여주는 것이 중요한 사이트를 구현하는데 용이합니다.

## 클라이언트사이드 렌더링 (CSR)

클라이언트사이드 렌더링은 최소한의 HTML과 javaScript를 다운로드 합니다. React의 렌더링 방식을 생각면 쉬울거 같습니다. `id ="root"`에 필요한 컴포넌트를 렌더링하는 것처럼 **동적인 페이지를 구현하는데 사용됩니다.**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="app.js"></script>
  </body>
</html>
```

### 동작 방식

1. 브라우저가 서버에서 최소한의 HTML과 javaScript를 다운받는다.
2. 브라우저에서 javaScript가 실행되어 HTMl 콘텐츠를 동적으로 생성하고 화면에 표시한다.

### 장점

- 빠른 페이지 전환: 첫 로딩 이후에는 서버 요청 없이 클라이언트에서 페이지를 동적으로 렌더링하기 때문입니다.
- 유연한 사용자 경험: 복잡한 UI와 실시간 업데이트에 적합합니다.
- 서버 부담 감소: 대부분의 작업이 클라이언트에서 이루어지므로 서버 부하가 줄어듭니다.

### 단점

- SEO 문제: 초기 HTML이 빈 껍데기일 경우, 검색 엔진이 페이지를 제대로 인덱싱하지 못할 가능성이 있습니다.
- 초기 로딩 시간 증가: 필요한 JavaScript 파일이 많으면 초기 로딩 속도가 느려질 수 있습니다.
- 브라우저 의존성: 사용자의 기기나 브라우저 성능에 따라 렌더링 속도가 달라질 수 있습니다.

## SEO란?

SEO는 웹사이트가 검색 엔진 결과 페이지에서 더 높은 순위에 노출되도록 최적화하는 과정입니다. 우리가 검색을 하면 검색 키워드에 맞는 웹페이지들이 상단에 순서대로 보이는걸 생각하면 될거 같습니다.

# Node.js

웹사이트가 검색 엔진 결과 페이지(SERP)에서 더 높은 순위에 노출되도록 최적화하는 과정입니다.

## Node.js 특징

### 비동기 및 이벤트 기반 구조

Node.js는 비동기 방식으로 작동하므로 요청이 완료될 때까지 기다리지 않고 다른 작업을 계속할 수
있습니다. 이벤트 기반으로 작동하여 효율적인 리소스 관리를 지원하며, 대규모의 동시 연결을
처리하는 데 적합합니다.

### 싱글 스레드, 논블로킹 I/O

Node.js는 싱글 스레드로 작동하지만, 논블로킹 I/O 모델을 사용해 여러 작업을 동시에 처리합니다.
이를 통해 메모리와 CPU 사용량을 절약하며 고성능을 제공합니다.

- 블로킹과 논블로킹 차이 : **호출된 함수가 호출한 함수에게 제어권을 주는냐 안주는냐로 구분된다고 합니다.**
- 비동기와 논블로킹 차이 : 비동기는 출력 순서와 관련된 개념이고 논블로킹이 병렬 실행과 관련된 개념이라고 합니다.

#### 블로킹과 논블로킹

![](https://velog.velcdn.com/images/ddclub12/post/c9604087-9784-4a31-b013-96d0f34be2df/image.png)

블로킹의 동작 방식은 다음과 같다.

1. A 함수가 B 함수를 호출하면 B에게 제어권이 넘어간다.
2. 제어권을 넘겨받은 B는 함수를 실행한다.
3. 이때 A는 B에게 제어권을 넘겨주었기 때문에 A 함수는 실행을 잠시 멈춘다. (Block)
4. B 함수가 실행이 끝나면 자신을 호출한 A에게 제어권을 돌려준다.
5. 제어권을 다시 받는 A 함수는 그 다음 작업을 실행한다.

반대로 논블로킹의 동작 방식은 다음과 같다.
![](https://velog.velcdn.com/images/ddclub12/post/99a51266-a3b6-4bfb-99fe-42281eafd8cd/image.png)

1. A 함수가 B 함수를 호출합니다.
2. 호출된 B 함수는 실행되지만, 제어권은 A 함수가 그대로 가지고 있습니다.
3. A 함수는 계속 제어권을 가지고 있기 때문에 B 함수를 호출한 이후에도 자신의 코드를 계속 실행합니다.

### 크로스 플랫폼

Node.js는 Windows, macOS, Linux 등 다양한 플랫폼에서 실행 가능하며, 이식성이 좋아 여러 환경에서
일관된 성능을 기대할 수 있습니다.

### 빠른 실행 속도

Node.js는 Google V8 JavaScript 엔진을 기반으로 하여 매우 빠르게 JavaScript 코드를 컴파일하고 실행
이로 인해 서버 측 작업의 성능이 뛰어납니다.

### 풍부한 모듈 및 npm

npm은 Node.js의 기본 패키지 관리자이며, 많은 오픈소스 모듈과 라이브러리를 제공하여 손쉽게 다양한
기능을 구현할 수 있습니다. 이를 통해 개발 시간을 절약할 수 있습니다.

```toc

```