---
emoji: 👨🏻‍💻
title: RBF 1회차 (Form, CSS 산텍지, Box 모델)- 1차 프로젝트 5팀
date: '2024-11-22 22:30:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# Form 이란

- 사용자의 입력값을 서버에 전달하기 위해 사용되는 input, button 태그의 필수 부모 태그
- Javascript에서 사용자 입력 값을 활용 하거나 필터링하여 다시 서버로 전달하는 메커니즘

## 동작 과정

1. 브라우저는 폼 태그에 입력된 데이터를 웹 서버로 보낸다 (GET 또는 POST 방식)
2. 웹 서버는 받은 데이터를 처리하기 위해 벡엔드 웹 프로그램으로 전달한다 (백엔드 웹 프로그램: Django, Node.js, Spring)
3. 웹 프로그램에서 처리된 데이터 결과에 따라 새로운 html 페이지를 웹 서버에 보낸다
4. 웹 서버는 받은 html 페이지를 브라우저에 보낸다
5. 브라우저는 받은 html 페이지를 렌더링하여 보여준다 (렌더링: HTML(구조) + CSS(디자인) + JavaScript(동작) 등 웹 리소스를 브라우저에 있는 렌더링 엔진이 해석하고 화면에 표시하는 과정)

## Form 태그 속성

1. action: 폼 데이터를 보낼 서버의 URL을 지정하는 속성
2. method: 데이터의 전송 방식을 지정하는 속성
   - GET: 폼의 데이터가 URL 뒤에 ?로 시작하는 쿼리 스트링 형식으로 추가된다
     - 장점
       1. URL에 데이터가 포함되므로 북마크 가능
       2. 간단한 데이터 조회 요청에 적합
       3. 서버의 캐시나 로그에 쉽게 기록 가능
     - 단점
       1. url에 데이터가 포함 되어있어 보안적으로 적합하지 않음
       2. url에 길이 제한이 있음
   - POST: 폼의 데이터가 URL 뒤에 보이지 않는다
     - 장점
       1. 데이터 길이에 제한이 없으며, 대량의 데이터를 전송 가능
       2. url에 데이터가 포함되어 있지 않아 보안적으로 적합
       3. 파일 업로드와 같은 복잡한 데이터를 전송하기에 적합
   - 단점
3. name: 폼을 식별하기 위한 이름을 지정하는 속성

## GET VS POST

| 구분 | GET                                                   | Post                                                   |
| ---- | ----------------------------------------------------- | ------------------------------------------------------ |
| 장점 | URL에 데이터가 포함되므로 북마크 가능                 | 데이터 길이에 제한이 없으며, 대량의 데이터를 전송 가능 |
|      | 간단한 데이터 조회 요청에 적합                        | url에 데이터가 포함되어 있지 않아 보안적으로 적합      |
|      | 서버의 캐시나 로그에 쉽게 기록 가능                   | 파일 업로드와 같은 복잡한 데이터를 전송하기에 적합     |
| 단점 | url에 데이터가 포함 되어있어 보안적으로 적합하지 않음 | 캐시나 북마크가 불가능.                                |
|      | url에 길이 제한이 있음                                | URL만으로 데이터를 확인하기 어려움.                    |

- 캐시: 캐시는 자주 사용하는 데이터를 임시로 저장하여 재사용함으로써 속도를 높이고 서버 부하를 줄이는 매커니즘
- 로그 : 시스템의 상태와 요청/응답 내역을 추적하고 분석할 수 있도록 기록하는 역할

# CSS 선택자

## 선택자 동작 원리

1. 선택자를 기반으로 DOM 트리를 탐색하여 조건에 부합하는 요소를 찾습니다
2. 우선순위 계산
3. 우선순위에 따라 적합한 스타일 적용

## 가상 선택자

- 가상 선택자는 HTML 요소의 상태 또는 구조적인 조건에 따라 선택할 수 있도록 해준다.

### 상태 선택자

- 선택한 HTML요소가 특별한 상태여야 만족해야 해당 스타일을 적용할 수 있다
- 다른 가상 선택자와 조합이 가능하다

1. `:hover:` 마우스가 요소 위에 올려졌을 때
2. `:focus:` 요소가 포커스를 받았을 때

- 발생조건
  1. 키보드로 탭(Tab) 키를 눌러 이동할때
  2. 마우스로 요소를 클릭했을때
- 활용예시

  1. 입력 필드 (ex - input:text )가 포커스 되었을때
  2. 버튼(button)요소가 포커스 되었을때

- focus 관련 추가 속성

  1. focus-visible: focus와는 다르게 Tab 키로만 눌러 포커스를 줄때만 스타일이 적용된다
  2. focus-within: 어떤 요소에 스타일을 적용하면 해당 요소를 포함한 그 내부에 요소 중에 하나가 포커스를 받으면 스타일이 적용된다

     - 활용 예시 코드

     ```html
     <div>
       <input />
       <button>검색</button>
     </div>
     ```

     ```css
     div:focus-within {
       outline: 2px solid red;
     }
     ```

     - 위 예시에서는 input 또는 button이 클릭이나 Tab키를 통해 포커스를 받으면 스타일이 적용된다

3. `:active:` 요소가 활성 상태일 때(예: 클릭 중)
4. `:checked:` 체크박스나 라디오 버튼이 선택되었을 때

## 구조 선택자

- HTML 요소의 위치나 관계를 기준으로 특정 요소를 선택해 스타일을 적용할 수 있다

### :nth-child(n)

- 부모 요소의 n번째 자식요소를 선택해 스타일 지정
- 만약 홀수를 지정하고 싶으면 n에 odd를, 짝수를 지정하고 싶으면 even을 지정하면 된다

```html
<ul id="test1">
  <li>테스트1</li>
  <li>테스트2</li>
  <li>테스트3</li>
  <li>테스트4</li>
  <li>테스트5</li>
  <li>테스트6</li>
</ul>
```

```css
#test1 li:nth-child(odd) {
  background-color: aqua;
}
```

테스트1,3,5 문단만 스타일지정

### :nth-of-type(n)

- 특정 태그 유형에서 n번째 요소를 선택한다. 단, 같은 부모 안에서 동일한 태그끼리만 세어 계산한다.

```html
<div id="test1">
  <pre>테스트1</pre>
  <div>테스트2</div>
  <div>테스트3</div>
  <div>테스트4</div>
  <div>테스트5</div>
  <pre>테스트6</pre>
</div>
<hr />
<br />
<div id="test2">
  <pre>테스트1</pre>
  <pre>테스트2</pre>
  <div>테스트3</div>
  <div>테스트4</div>
  <div>테스트5</div>
  <div>테스트6</div>
</div>
```

```css
div pre:nth-of-type(2) {
  background-color: aqua;
}
```

test1에서는 테스트6 문단이, test2에서는 테스트2 문단이 스타일 적용이 된다

### 특수 선택자 root

참고링크: <https://dony0720.github.io/Programmers/Day4/#root-%EC%8A%A4%ED%83%80%EC%9D%BC-%EC%A7%81%EC%A0%91-%EC%A0%95%EC%9D%98%EC%99%80-%EB%B3%80%EC%88%98-%EC%84%A0%EC%96%B8%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90>

# CSS 선택자 성능 최적화를 위한 팁

## 선택자 성능을 저하시키는 요인

- 복잡한 선택자 체인: 깊은 후손 선택자(div ul li span)는 브라우저가 많은 노드를 탐색하도록 만듭니다.
- 전체 선택자 사용: \* 선택자는 모든 요소를 선택하므로 비효율적입니다.
- 잘못된 위치에서의 가상 선택자: 구조 기반 선택자가 복잡한 DOM 구조와 결합될 경우 성능 문제가 발생할 수 있습니다.

## 성능 최적화를 위한 방법

1. ID와 클래스 선택자를 우선적으로 사용: 브라우저는 ID 선택자를 가장 빠르게 처리하며, 그다음 클래스 선택자를 처리합니다.

```css
/* 비효율적: 태그 기반 */
div ul li span {
  color: blue;
}

/* 효율적: 클래스 기반 */
.highlight {
  color: blue;
}
```

2. 후손 선택자보다 자식 선택자를 사용: 후손 선택자(div ul li)는 전체 DOM 트리를 탐색하지만, 자식 선택자(div > ul > li)는 탐색 범위를 줄입니다.

```css
/* 비효율적 */
div ul li {
  color: red;
}

/* 효율적 */
div > ul > li {
  color: red;
}
```

- 자손과 후손의 차이점

  ```html
  <div class="parents">
    <h1>나는 부모다.</h1>

    <div class="child">
      <h1>나는 자식이다.</h1>

      <div class="greatGrandchild">
        <h1>나는 증손자다.</h1>
      </div>
    </div>
  </div>
  ```

  - 후손 선택: **선택 태그 안에 들어가 있는 모든 것**

  ```css
  .parents h1 {
    color: blue;
  }
  ```

  parents, child, greatGrandchild class 자식에 있는 모든 h1태그에 스타일이 적용됨

  - 자손 선택: 선택 태그 바로 아래 계층에 있는 것들

  ```css
  .parents > h1 {
    color: blue;
  }
  ```

  parents class에 있는 h1태그에만 스타일이 적용된다

3. 가장 가까운 공통 조상 활용: 선택자의 범위를 좁히기 위해 요소와 선택자 사이에 가장 가까운 공통 조상을 사용할 수 있다. 이렇게 하면 브라우저가 탐색해야 하는 범위가 줄어들어 더 빠른 선택이 가능해진다.

```html
<div class="card-list">
  <div class="card">
    <h2>제목</h2>
    <p>내용</p>
  </div>
  <div class="card">
    <h2>다른 제목</h2>
    <p>다른 내용</p>
  </div>
</div>
```

```css
/* 비효율적인 선택자 */

h2 {
  font-size: 20px;
  color: blue;
}
/* 후손 선택 */
.card-list div p {
  color: gray;
}
```

위 예시에서의 문제점은 다음과 같다

- h2는 문서 전체를 탐색한다
- .card-list div p는 div와 p 사이에 공통 조상이 없어 탐색 범위가 넓습니다.

```css
.card-list > .card > h2 {
  font-size: 20px;
  color: blue;
}

.card-list > .card > p {
  color: gray;
}
```

개선사항은 다음과 같다

- .card-list를 기준으로 탐색 범위를 제한.
- 자식 선택자(>)를 사용해 탐색 범위를 추가로 좁힘.

# CSS 박스 모델

![](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/box-model.png)

참고 링크: https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/box-model.png

## Content : 실제 컨텐츠가 표시되는 영역

- width와 height 속성을 사용해 크기를 조정할 수 있습니다.
- 블록요소의 높이 너비를 설정할 수 있다(inline-block 포함)

```html
<div class="content1">content1 영역입니다.</div>
```

```css
.content1 {
  width: 200px;
  height: 100px;
}
```

## Padding : 콘텐츠와 테두리(border) 사이의 내부 여백

- 콘텐츠와 테두리(border) 사이의 내부 여백입니다
- 주요 옵션 : 전체, 상, 하, 좌, 우 따로 지정할수 있다. 하지만 전체적인 스타일 적용후 따로 특정 영역에 스타일 적용하는 것을 추천한다(상,하,좌,우 각각 스타일 지정을 했을때 헷갈릴 우려가 있기 때문에)
- 특정영역에 단독으로 스타일 지정을 하고 싶을때 -top, -bottom, -left, -right를 붙여 값을 설정해주면 된다

```css
.padding1 {
  /* 모든 방향에 30px */
  padding: 30px;
}
.padding2 {
  /* 상,하: 50px 좌,우: 20px */
  padding: 50px 20px;
}
.padding3 {
  /* 상:50px 좌,우: 50px. 하: 100px*/
  padding: 10px 50px 100px;
}
.padding4 {
  /* 상: 10px 우:50px 하:100px 좌:200px */
  padding: 10px 50px 100px 200px;
}
.padding5 {
  /* 실무적이고 확실한 방법 */
  padding: 30px;
  padding-top: 100px;
}
```

## Border : 패딩과 마진 사이에 있는 영역

- 아래와 같이 스타일 적용시 일일 속성을 지정해줘야 하는 비효율적인 부분이 있음

```css
.border1 {
  border-style: solid;
  border-width: 2px;
  border-color: black;
}
```

- border 속성 사용시 한번에 style, width, color 스타일을 한번에 지정해 줄 수 있음

```css
.border1 {
  border: 1px solid black;
}
```

## Margin : 요소와 이웃한 요소 사이의 외부 여백

- padding처럼 지정하는 방법이 동일하다
- '-'(마이너스)가 사용 되는 옵션
- auto 속성이 있으면 좌우 정렬시 활용된다

```css
.margin1 {
  /* 모든 방향에 30px */
  padding: 30px;
}
.margin2 {
  /* 상,하: 50px 좌,우: 20px */
  padding: 50px 20px;
}
.margin3 {
  /* 상:50px 좌,우: 50px. 하: 100px*/
  padding: 10px 50px 100px;
}
.margin4 {
  /* 상: 10px 우:50px 하:100px 좌:200px */
  padding: 10px 50px 100px 200px;
}
.margin5 {
  /* 실무적이고 확실한 방법 */
  padding: 30px;
  padding-top: 100px;
}
.margin6 {
  /* 마이너스 사용시 간격이 좁혀진다 */
  margin-top: -30px;
  margin-left: -50px;
}
```

## Border-box

### 기본 박스 모델

- width와 height는 **콘텐츠(content)**의 크기만 정의합니다.
- 패딩, 테두리, 마진은 별도로 추가됩니다.

```css
div {
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 5px solid black;
}
```

1. 총 너비 = 100px(콘텐츠) + 10px(좌우 패딩) + 5px(좌우 테두리) = 130px
2. 총 높이 = 100px(콘텐츠) + 10px(좌우 패딩) + 5px(좌우 테두리) = 130px

### Box-sizing: border-box

- width와 height가 콘텐츠, 패딩, 테두리의 총 크기를 포함합니다(즉 width x height의 크기를 유지한다)

```css
div {
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 5px solid black;
  box-sizing: border-box;
}
```

1. 총 너비, 총 높이 = 100px (모든 요소 포함)
2. content의 너비, 높이 = 100px - 5px(border) - 10px(padding) = 85px

```toc

```
