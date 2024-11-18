---
emoji: 👨🏻‍💻
title: Day 1 에멧(emmet),
date: '2024-11-18 17:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

## 에멧(emmet)

### 에멧(emmet) 정의

에멧은 HTML과 CSS를 빠르게 타이핑 할 수 있는 문법이며 태그 뿐만 아니라 id,class,속성 값에 규칙 적으로 자동 완성 할 수 있어
html을 편리하게 구성 할 수 있다.

### 에멧 문법 예시

#### Child(자식) : >

에멧 문법

```
div>ul>li
```

결과

```js
<div>
  <ul>
    <li></li>
  </ul>
</div>
```

- 위와 같이 코드를 작성하게 되면 아래와 같이 div -> ul -> li 의 순서로 자식요소를 생성한다

#### Sibling(형제) : +

에멧 문법

```
div+p+bq
```

결과

```js
<div></div>
<p></p>
<blockquote></blockquote>
```

- 작성 순서대로 태그를 생성한다

#### 자식 + 형제 응용

에멧 문법

```
div+div>p>span+em
```

결과

```js
<div></div>
<div>
<p><span></span><em></em></p>
</div>
```

- 처음 div는 그냥 생성되고 두번째 div는 p -> span 의 순서로 자식 태그를 생성한다

#### Climb-up(올라가기) : ^

에멧 문법

```
div+div>p>span+em^bq
```

결과

```js
<div></div>
<div>
<p><span></span><em></em></p>
<blockquote></blockquote>
</div>
```

- blockquote 태그가 p의 자식 요소로 생성되지 않고 두번째 div의 자식요소로 생성된다

#### Multiplication(곱셈) : \*

에멧 문법

```
ul>li*5
```

결과

```js
<ul>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

- 곱셉을 통해 li태그가 5개 생성된다

#### Grouping (그룹핑) : ( )

에멧 문법

```
div>(header>ul>li*2>a)+footer>p
```

결과

```js
<div>
  <header>
    <ul>
      <li>
        <a href=""></a>
      </li>
      <li>
        <a href=""></a>
      </li>
    </ul>
  </header>
  <footer>
    <p></p>
  </footer>
</div>
```

- header 태그 안에 ul 태그를 자식으로 생성한다
- ul 태그 안에 a 태그를 자식으로 하는 li 태그를 2개 생성한다
- footer 태그에 p 태그를 자식으로 생성한다

#### Id와 Class

에멧 문법

```
div#header+div.page+div#footer.class1.class2.class3
```

결과

```js
<div id="header"></div>
<div class="page"></div>
<div id="footer" class="class1 class2 class3"></div>
```

- header라는 id 값을 가진 div 태그를 생성
- page라는 class 값을 가진 div 태그 생성
- footer라는 id 값과 class1, class2, class3 라는 3개의 class 값을 가진 한개의 div 태그를 생성한다

#### Custom attributes (속성)

에멧 문법

```
td[title="Hello world!" colspan=3]
```

결과

```js
<td title="Hello world!" colspan="3"></td>
```

#### Text (속성)

에멧 문법

```
div{text value}
```

결과

```js
<div>text value</div>
```

#### Item numbering : $

에멧 문법

```
ul>li.item$*5
```

결과

```js
<ul>
  <li class="item1"></li>
  <li class="item2"></li>
  <li class="item3"></li>
  <li class="item4"></li>
  <li class="item5"></li>
</ul>
```

- 클래스의 값을 1tem 1~5 까지 순차적으로 생성한다

#### Item numbering : $$$

에멧 문법

```
ul>li.item$$$*5
```

결과

```js
<ul>
  <li class="item001"></li>
  <li class="item002"></li>
  <li class="item003"></li>
  <li class="item004"></li>
  <li class="item005"></li>
</ul>
```

#### Item numbering2: @ + $

에멧 문법

```
ul>li.item$@-*5
```

결과

```js
<ul>
  <li class="item5"></li>
  <li class="item4"></li>
  <li class="item3"></li>
  <li class="item2"></li>
  <li class="item1"></li>
</ul>
```

- 클래스의 값을 item 5부터 1까지 내림차순으로 생성한다

- **_$$$_** 를 세자리 숫자로 여겨 클래스의 값을 item 001~005까지 순차적으로 생성한다

## HTML

### HTML 정의와 특징

HTML이란?

- 웹에서 정보를 표현할 목적으로 만든 마크업 언어
- 웹 페이지를 작성하기 위해 사용되는 언어이며 웹 페이지의 구조를 구성한다.
- 문자열과 다양한 태그들로 구성

마크업과 마크업 언어

- 마크업(태그): 문서의 논리적인 구조를 정리하고 웹에서 어떤 형태로 보일 것인지 지시하는 역할
- 마크업 언어: 마크업의(태그)의 형식과 규칙을 정의한 언어 (예시: HTML,XMl)

HTML의 특징은 다음과 같다.

- 구조적 설계 지원 (시멘틱)/ 그래픽 및 멀티미디어 기능 강화
- CSS3 및 Javascript 지원/ 다양한 확장 기능 및 API 제공
- Mobile지원 및 장치 접근 가능 (GPS, 카메라, 블루투스 등)
- 웹 브라우저가 서버와 양방향 통신 가능 (Web Socket)

### 구성요소

예시

```
<h1 class = "header"> Hello HTML</h1>
```

| 구성요소 | 내용                                                                                                             |
| -------- | ---------------------------------------------------------------------------------------------------------------- |
| 태그     | <>로 묶인 명령어, 시작태그(<태그>)와 종료태그(</태그>)를 한쌍으로 이용한다. 위 예시에서는 h1이 태그로 사용되었다 |
| 요소     | 태그가 실제 브라우저에서 렌더링된 인스턴스 상태를 의미한다                                                       |
| 텍스트   | 태그를 제외한 순수 Text를 의미한다                                                                               |
| 속성     | 요소의 시작태그에만 사용한다/ 여러개의 속성값을 사용할 수 있다 / 속성의 구분은 공백을 통해 구분한다              |
| 속성값   | 속성이 가지는 값(예시에서는 header)/ 값 입력시 ""를 사용한다                                                     |

### 주의 사항 🚨🚨

- 태그는 대소문자를 구분하지 않으나 소문자로 작성하는것을 권장한다
- 시작 태그로 시작하면 반드시 종료태그로 종료해야한다

```html
<!DOCTYPE html>
<html lang="ko">
  <head> </head>
  <body></body>
</html>
```

위 코드는 기본적인 HTML의 구조이고 특징은 다음과 같다

- head는 문서의 각종 정보와 문서 자체에 대한 설명이 있다 (예시 태그: title, meta, link, style, script)
- body는 화면에 출력해서 보여주는 모든 정보,내용이 포함된다 / head에 사용되는 태그를 제외하고 모든 태그를 body에서 사용한다.

```toc

```
