---
emoji: 👨🏻‍💻
title: WTL 2회차 브라우저 이벤트, 버블링 & 캡쳐링 - 1차 프로젝트 5팀
date: '2024-12-04 22:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 브라우저 이벤트

브라우저 이벤트란 브라우저 내에서 특정 액션을 말한다. 클릭, 스크롤, CSS 애니메이션이 종료되었을때와 같은 액션을 예로 들 수 있을 것이다.

## 이벤트 종류

### 마우스 이벤트

- click : 마우스 왼쪽을 클릭했을때
- contextmenu: 마우스 오른쪽을 클릭했을때
- mouseover : 마우스 커서를 요소 위로 움직였을때
- mouseup : 마우스 커서가 요소 밖으로 나갈때 (쉽게 hover를 생각하면 좋을듯 같다)
- mousedown : 마우스 왼쪽을 누르고 있을때
- mousemove : 마우스 왼쪽이 뗄 때 (click = mousedown & mouseup)

### 폼 요소 이벤트

- submit : 데이터가 전송됐을때
- focus: input 요소가 활성화 됐을때

### 키보드 이벤트

- keydown : 키보드를 눌렀을때
- keyup : 키보드 키를 뗄 때

### Dom 이벤트

- DOMContentLoaded : 페이지 로드가 다 완료될때

### CSS 이벤트

- transitionend : CSS 애니메이션이 종료되었을때

## 이벤트 핸들러

이벤트 핸들러란 **이벤트가 입력될때 작동하는 함수이다.** 이벤트를 적용하는 방법은 HTML태그 내에서의 인라인 방식 , addEventListener

### HTML 인라인 방식

```html
<input value="클릭해 주세요." onclick="alert('클릭!')" type="button" />

<script>
  function sayHello() {
    console.log('안녕하십니까');
  }
</script>

<input value="클릭해 주세요." onclick="sayHello()" type="button" />
```

- onclick은 해당 요소에서 함수를 동작시키 위한 이벤트이다. 버튼을 click 하게 되면 해당 요속가 이벤트를 입력받고 이벤트에 할당된 함수를 동작시킨다.
- onclick 과 같이 이벤트를 등록하기 위해서는 **on + event명** 으로 작성해야 한다. 예시로는 onmousedown, onkeydown 같이 작성해주어야 한다.
- 만약 코드가 길다면 함수를 따로 작성해 함수를 호출해주어도 된다.

#### this 사용

```html
<button onclick="alert(this.innerHTML)">클릭해 주세요.</button>
```

this.innerHTML에서 this는 button이므로 버튼을 클릭하면 버튼 안의 콘텐츠가 얼럿창에 출력됩니다

### DOM 프로퍼티

Javascript에서 요소의 id 또는 class 값을 가져와서 적용하는 방식이다.

```html
<button class="btn">Click me</button>
<script>
  const btn = document.querySelector('.btn');

  function sayHello() {
    console.log('안녕하세요');
  }
  function Bye() {
    console.log('안녕히가세요');
  }
  // 이벤트 핸들러 프로퍼티 방식은 이벤트에 하나의 이벤트 핸들러만을 바인딩할 수 있다
  // 첫번째 바인딩된 이벤트 핸들러 => 실행되지 않는다.
  btn.onclick = sayHello;

  // 두번째 바인딩된 이벤트 핸들러
  btn.onclick = Bye; //=> 실행됨
</script>
```

출처: https://inpa.tistory.com/entry/JS-📚-이벤트-💯-총-정리#ui_event [Inpa Dev 👨‍💻:티스토리]

주의점: 이벤트에 함수를 등록시 ` btn.onclick = Bye()`를 하게 되면 함수 호출의 결과가 할당되는 것이기 때문에 예상과 다르게 동작될 것이다. 반드시 위와 같이 함수명만 적어야 등록이 된다.

### addEventListener

DOM 프로퍼티와 생김새가 비슷하지만 addEventListener는 한 요소에 여러 함수를 할당할 수 있다.

```html
<button class="btn">Click me</button>
<script>
  const btn = document.querySelector('.btn');

  function sayHello() {
    console.log('안녕하세요');
  }
  function welcome() {
    alert('welcome');
  }
  btn.addEventListener('click', sayHello);
  btn.addEventListener('click', Bye);
</script>
```

addEventListener(type, listener) 인자에 대해서 설명하는 것이 좋을거 같다

type: 요소의 이벤트 수신의 역할을 담당한다.
listener: type에서 작성된 이벤트가 들어왔을때 함수를 실행한다. 위 예시에서는 버튼을 click을 했을때 버튼은 click 이벤트를 수신 후에 sayHello()와 welcome() 함수를 실행시킨다.

# 버블링과 캡처링

## 버블링

버블링: 자식 요소에서 발생된 핸들러 함수가 같은 이벤트를 가진 최상단의 조상 요소들의 핸들러 함수를 발생시킨다.

```html
<div id="Grand">
  <div id="parent">
    <button id="child1">Click Me</button>
    <button id="child2">Click Me2</button>
  </div>
</div>

<script>
  document.getElementById('Grand').addEventListener('click', (event) => {
    console.log('Grand clicked!');
    console.log(event.target);
  });
  document.getElementById('child1').addEventListener('click', (event) => {
    console.log('Child clicked!');
    console.log(event.target);
  });

  document.getElementById('parent').addEventListener('contextmenu', (event) => {
    console.log('Parent clicked!');
    console.log(event.target);
  });

  document.getElementById('child2').addEventListener('contextmenu', (event) => {
    console.log('Child2 clicked!');
    console.log(event.target);
  });
</script>
```

Grand & child1 , parent & child2

- Grand & child1는 **click 이벤트를** ,parent & child2는 **contextmenu 이벤트를** 가지고 있다. 그래서 자식 요소인 child1을 클릭하게 되면 버블링으로 인해 Grand에 할당된 핸들러 함수가 의도치 않게 동작된다.

## 형제관계에서의 버블링

형제 요소 간의 직접적인 이벤트 전파는 없지만, 형제 요소들이 같은 부모를 공유하기 때문에 부모 요소를 통해 간접적으로 이벤트를 처리할 수 있다.

```html
<div id="parent">
  <button id="sibling1">Sibling 1</button>
  <button id="sibling2">Sibling 2</button>
</div>

<script>
  // 부모 요소에 리스너 등록
  document.getElementById('parent').addEventListener('click', (event) => {
    console.log(`Parent received event from: ${event.target.id}`);
  });

  // 첫 번째 버튼에 리스너 등록
  document.getElementById('sibling1').addEventListener('click', () => {
    console.log('Sibling 1 clicked!');
  });

  // 두 번째 버튼에는 리스너 없음
</script>
```

실행 결과

1. Sibling 1 클릭 시

- "Sibling 1 clicked!" 출력 (Sibling 1 자체 리스너 실행)
- "Parent received event from: sibling1" 출력 (버블링으로 부모 리스너 실행)

2. Sibling 2 클릭 시

- "Parent received event from: sibling2" 출력 (Sibling 2에는 리스너가 없지만 부모로 버블링됨)

3. 형제 간 이벤트는 전파되지 않음

- Sibling 1의 클릭 이벤트는 Sibling 2로 직접 전파되지 않습니다.
- 대신 공통 부모(parent)를 통해 이벤트를 처리할 수 있습니다.

## 캡쳐링

캡쳐링은 버블링과는 다르게 상위 요소에서 하위요소로 이동하는 개념이다.

### 기본 문법

캡처링 단계에서 이벤트를 잡아내려면 addEventListener의 capture 옵션을 true로 설정해야 한다.

```js
// 캡처링 동작
element.addEventListener('click', (e) => { ... }, true);

// 아래 같이 {capture: true} 대신, true를 써줘도 됩니다.
element.addEventListener('click', (e) => { ... }, {capture: true});

```

## 버블링 & 캡처링 전파 막기

### e.stopPropagation( ), e.stopImmediatePropagation( )

- e.stopPropagation() : ​이벤트 전파 중지
- e.stopImmediatePropagation() : 이벤트 전파 중지 + 형제 이벤트 실행 중지

출처: https://inpa.tistory.com/entry/JS-📚-버블링-캡쳐링#이벤트_캡처링 [Inpa Dev 👨‍💻:티스토리]

```js
document.getElementById('parent').addEventListener('contextmenu', (event) => {
  console.log('Parent clicked1');
  event.stopPropagation();
  console.log(event.target);
});

// 한 요소에 적용된 다수의 핸들러 막을때
document.getElementById('parent').addEventListener('contextmenu', (event) => {
  console.log('Parent clicked2');
  if (조건) {
    event.stopImmediatePropagation();
  }
  console.log(event.target);
});
```

### Event.preventDefault( )

특정 요소에 이벤트가 발생될때 버블링 & 캡쳐링과 브라우저가 수행하는 기본 동작을 막는다.

1. 체크박스 체크 불가
2. a 태그 클릭시 href 링크로 이동 불가
3. form 태그 자식 요소의 데이터 전송후 페이지 리로드 불가

- form 태그의 기본 동작을 막지 않으면 데이터 전송후 페이지가 바로 리로드 되버려 데이터의 값이 현재 페이지에 머무르지 못하고 사라진다. form 태그 자식요소에 있는 데이터를 활용하고 싶다면 form 태그의 기본 동작을 막아야한다.

4. ​event.preventDefault() : 이벤트 전파 중지 + 형제 이벤트 실행 중지 + 이벤트 기본 동작 중지

### 기본 문법

```js
element.addEventListener('event', function (event) {
  event.preventDefault();
  // 원하는 동작을 작성
});
```

### 예시

1. 링크 클릭 기본 동작 막기

```html
<a href="https://example.com" id="myLink">이동</a>
<script>
  const link = document.getElementById('myLink');
  link.addEventListener('click', function (event) {
    event.preventDefault();
    console.log('링크 클릭 기본 동작이 막혔습니다!');
  });
</script>
```

2. 폼 제출 기본 동작 막기

```html
<form id="myForm">
  <input type="text" name="name" />
  <button type="submit">제출</button>
</form>
<script>
  const form = document.getElementById('myForm');
  form.addEventListener('submit', function (event) {
    event.preventDefault();
    console.log('폼 제출 기본 동작이 막혔습니다!');
  });
</script>
```

3. 조건부 기본 동작 막기

```js
document.addEventListener('keydown', function (event) {
  if (event.key === 'F5') {
    // F5 키를 눌렀을 때
    event.preventDefault(); // 새로고침 방지
    alert('새로고침이 차단되었습니다!');
  }
});
```

## event.target

- this: 핸들러 함수가 할당된 요소를 참조한다.
- event.target : 실제 이벤트를 받아 핸들러 함수의 코드가 적용되는 곳

```html
<form id="form">
  FORM
  <div>
    DIV
    <p>P</p>
  </div>
</form>

<script>
  const form = document.getElementId('form');
  form.onclick = function (event) {
    event.target.style.backgroundColor = 'yellow';

    // chrome needs some time to paint yellow
    setTimeout(() => {
      alert('target = ' + event.target.tagName + ', this=' + this.tagName);
      event.target.style.backgroundColor = '';
    }, 0);
  };
</script>
```

- form 태그에 핸들러가 할당되어 있어서 this는 form태그를 가리킨다.

참고 문헌 : https://ko.javascript.info/bubbling-and-capturing

```toc

```
