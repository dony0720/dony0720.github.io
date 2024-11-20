---
emoji: 👨🏻‍💻
title: Day 3 form 태그, button 태그
date: '2024-11-20 17:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# Form

- 사용자로부터 text 및 각종 입력을 전달받아 page가 지정한 서버로 전달(요청)하는 태그
- 주요한 form : text, pw, textarea, button, summit, radio, select 등

## 주요 Form

주요한 form: text, password, textarea, button, submit 등

```html
<form action="#" method="get" name="formName">
  <label for="userId">아이디</label>
  <input type="text" name="memberId" id="userId" />

  <label for="password">패스워드</label>
  <input type="password" name="password" id="password" />

  <input type="submit" value="제출" />
</form>
```

- action : 전달할 서버의 url, #은 본인의 페이지를 다시 요청하는 방법
- method : 전달할 방식을 선택, get은 url을 통한 노출, post는 url과 별개로 데이터를 전달, 생략하게 되면 디폴트 값은 **get**이지만 명시적으로 표시하는것을 권장한다
- input-id : html 레벨에서 고유의 id를 가지는 속성, 중복될수 없다!
- input-name : form에서 input 파라메터 전달시 사용될 파라메터의 이름,서버에서 활용 (서버에 id의 값이 아닌 name의 값이 전달된다)
- ※ id와 name은 일치하는게 보편적이지만, 다르게 해도 문제는 없다. 각자식별만 잘하면 된다.
- form 요소에 레이블(명칭)을 붙이기 위한 태그 레이블을 클릭하면 입력창으로 커서가 활성화(포커스 상태)된다.
- 레이블 : 입력 창 옆에 붙여 놓는 문구 (예 : 비밀번호, 아이디 등)

### 결과

![form 태그 동작 결과](Day3_image/Day3_form_result.png)

## button

### input-button type 활용

- 단점: css 적용이 어렵다

```html
<input type="submit" value="제출" />
<input type="button" value="버튼" onclick="alert('버튼클릭');" />
<input type="reset" value="리셋" />
```

### button 태크 활용

- 버튼을 태그로 표현해 활용하는 방법, 기능은 동일하나 css로 활용하기 편리하다

```html
<button type="submit">제출</button>
<button type="button" onclick="alert('버튼 클릭!')">버튼</button>
<button type="reset">리셋</button>
```

## 선택 관련 태그

- radio 버튼은 여러 값 중 하나만 선택해서 단일 값만 선택 가능
- checked: input이 checked 되어 있는 상태로 렌더링된다.

```html
<form action="" method="get">
  <input type="radio" name="gender" id="gender-male" value="m" checked />
  <label for="gender-male">남성</label>

  <input type="radio" name="gender" id="gender-female" value="f" />
  <label for="gender-female">여성</label>

  <input type="submit" value="제출" />
</form>
```

### 결과

![type ="radio" 결과](Day3_image/Day3_radio_result.png)

## checkBox

- 체크 박스의 경우 다중 값 선택이 가능
- 특징: 여러개의 name을 동시에 보낼 수 있다.(서버에서는 리스트꼴로 처리 필요)

```html
<form action="" method="get">
  <input type="checkbox" name="hobby" id="music" value="music" />
  <label for="music">음악감상</label>

  <input type="checkbox" name="hobby" id="game" value="game" checked />
  <label for="game">게임</label>

  <input type="checkbox" name="hobby" id="book" value="book" />
  <label for="book">독서</label>

  <input type="checkbox" name="hobby" id="health" value="health" checked />
  <label for="health">헬스</label>

  <input type="submit" value="제출" />
</form>
```

### 결과

![checkBox 동작 결과](Day3_image/Day3_checkBox_result.png)

## select

- 여러 값을 선택할때 활용하는 태그
- value 값이 없으면 표현값(텍스트)이 value로 대체된다
- selected: checked와 비슷하게 해당 옵션이 선택된 상태로 렌더링된다
- select 태그는 반드신 선택 옵션인 option 태그와 같이 사용해야한다

```html
<form action="" method="get">
  <label for="nation2">국가2</label>
  <select name="nation2" id="nation1">
    <option value="us">미국</option>
    <option value="cs">중국</option>
    <option value="jp">일본</option>
    <option value="ko" selected>한국</option>
  </select>
</form>
```

### 결과

![select 동작 결과](Day3_image/Day3_select_result.png)
