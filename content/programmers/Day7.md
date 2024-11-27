---
emoji: 👨🏻‍💻
title: Day 7 미디어 쿼리
date: '2024-11-26 16:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# CSS 미디어 쿼리

- 웹 페이지를 다양한 기기와 화면 크기에서 최적화하기 위해 CSS 스타일을 조건부로 적용하는 기능이다
- 반응형 웹 디자인(Responsive Web Design)의 핵심 도구로, 화면 크기, 해상도, 색상 모드 등 다양한 기기 특성에 따라 스타일을 변경할 수 있다

## 기본 문법

```css
@media (조건) {
  /* 조건에 해당할 때 적용될 스타일 */
}
```

- 조건 부분이 만족될때 해당 스타일이 적용된다

### 예시

```css
body {
  font-size: 16px;
}

@media (max-width: 768px) {
  body {
    font-size: 14px;
  }
}
```

- 화면 너비가 768px 이하일 경우에 font-size 14px이 적용된다

## 미디어 쿼리 조건

### max-width / min-width

- max-width: 화면 너비가 특정 값보다 작거나 같을 때 적용된다
- min-width: 화면 너비가 특정 값보다 클 때 적용된다

```css
/* 768px 이하일 때 스타일 적용 */
@media (max-width: 768px) {
  /* 스타일 */
}

/* 1024px 이상일 때 스타일 적용 */
@media (min-width: 1024px) {
  /* 스타일 */
}
```

### max-height / min-height'

- 화면 높이에 따라 스타일을 적용한다

```css
@media (max-height: 600px) {
  /* 높이가 600px 이하일 때 적용 */
}
```

### 복합조건

- 여러 조건을 논리 연산자(and, not, only)로 조합 가능하다

```css
@media (min-width: 768px) and (max-width: 1024px) {
  /* 화면 너비가 768px 이상 1024px 이하일 때 */
}
```

```css
@media not (orientation: landscape) {
  body {
    background-color: lightblue; /* 세로 모드일 때 적용 */
  }
}
```

```css
@media only screen and (min-width: 768px) and (max-width: 1024px) {
  body {
    background-color: lightgreen;
    /* 디스플레이 화면이 있고 너비가 768px ~ 1024px인 디바이스에만 스타일 적용 */
  }
}
```

```toc

```
