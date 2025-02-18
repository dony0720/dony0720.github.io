---
emoji: 👨🏻‍💻
title: Day 57 Vue event
date: '2025-02-18 23:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# Event

- vue에서는 v-on 디렉티브(@ 기호)를 사용하여 DOM 이벤트를 감지하고 핸들러를 실행한다.
- 컴포지션 API에서는 setup() 함수 내부에서 이벤트 핸들러를 정의하고 바인딩 한다.

## 이벤트 처리

### 이벤트 처리 - 인라인 핸들러 방식

- v-on을 활용하여 Vue와 바인딩된 객체 활용할 수 있는 script를 생성하여 처리

```vue
<script setup>
import { ref } from 'vue';

const amount = ref(0); // 금액
const balance = ref(0); // 잔고
</script>

<template>
  <div class="child">
    금액 : <input type="text" v-model.number="amount" />
    <button
      @click="
        balance += amount;
        amount = 0;
      "
    >
      입금
    </button>
    <button
      @click="
        balance -= amount;
        amount = 0;
      "
    >
      출금
    </button>
    잔고 : {{ balance }}
  </div>
</template>
```

### 이벤트 처리 - 메서드 핸들러

- `@`를 통해 Vue 내부의 메서드 핸들러와 연결하는 방식이다.
- 긴 이벤트 처리에도 적합하고 Vue 코드에서 이벤트 처리 코드를 작성 가능하다.
- 가급적 해당 방법을 사용하는 것을 권장, 사유는 코드 관리가 편해진다.

```vue
<script setup>
import { ref } from 'vue';

const amount = ref(0); // 금액
const balance = ref(0); // 잔고

const deposit = () => {
  if (amount.value <= 0) {
    alert('0보다 큰 값을 입력하세요.');
    return;
  }
  balance.value += amount.value;
  amount.value = 0;
};

const withdraw = () => {
  if (amount.value <= 0) {
    alert('0보다 큰 값을 입력하세요.');
  } else if (amount.value > balance.value) {
    alert('잔액이 부족합니다.');
  } else {
    balance.value -= amount.value;
    amount.value = 0;
  }
};
</script>

<template>
  <div class="child">
    금액 : <input type="text" v-model.number="amount" /><br />
    <button @click="deposit">입금</button>
    <button @click="withdraw">출금</button><br />
    <b>잔고 : {{ balance }}</b
    ><br />
  </div>
</template>
```

### 이벤트 처리 - 핸들러 + input 이벤트

- 일반적인 이벤트 핸들러를 생성하면 (e)=>{} 타입으로 생성되어 e 객체 활용 가능 <br>
- 만일, 사용자가 정의한 인자와 event 객체를 활용하고 싶은 경우, $event로 인자 처리가 가능 <br>

```vue
<script setup>
import { ref } from 'vue';

const value1 = ref('');
const value2 = ref('');

const changeValue = (e) => {
  value2.value = e.target.value;
};

const userClickEvent = (msg) => {
  alert(msg);
};

const userClickEvent2 = (msg, event) => {
  event.preventDefault();
  alert(`${msg}, ${event.target.innerText}`);
};
</script>

<template>
  <div class="child">
    <h3>인라인 이벤트 핸들러에서 e처리 방법</h3>
    value1 : {{ value1 }}<br />
    <input
      type="text"
      :value="value1"
      @input="
        (e) => {
          value1 = e.target.value;
        }
      "
    />

    <h3>함수로 분리한 이벤트 핸들러에서 e처리 방법</h3>
    value2 : {{ value2 }}<br />
    <input type="text" :value="value2" @input="changeValue" />

    <h3>사용자가 정의한 인자 전달 예제</h3>
    <button @click="userClickEvent('message 1입니다.')">사용자 정의 인자 전달</button>

    <h3>사용자가 정의한 인자 + event => $event 인자 전달</h3>
    <button @click="userClickEvent2('message 2입니다.', $event)">사용자 정의 인자 + event</button>
  </div>
</template>
```

## 이벤트 수식어

### 기본적인 수식어

- .stop : 이벤트 전파 중지 (event.stopPropagation())
- .prevent : 기본 동작 방지 (event.preventDefault())
- .self : 이벤트가 자기 자신에서만 발생할 때 실행
- .capture : 캡처 단계에서 실행
- .once : 한 번만 실행됨
- .passive : event.preventDefault()가 있어도 기본 동작을 수행

사용은 아래와 같이 사용하면 된다.

```
<script setup>

const doStop = () => alert('doStop 클릭, 이벤트 전파 안됨!');
const doThat = () => alert("doThat 클릭!");

</script>

<template>
    <button @click.stop="doStop">이벤트가 전파 방지 버튼</button> <br>

    <!-- 여러 수식어 조합 -->
    <button @click.stop.prevent="doThat">전파 + 기본동작 방지</button><br><br>
</template>

```

### 마우스 클릭 관련

- .left : 왼쪽 버튼 클릭
- .right : 오른쪽 버튼 클릭
- .middle : 가운데 버튼 클릭

```vue
<script setup>
const leftClick = () => alert('왼쪽 클릭됨!');
const rightClick = () => alert('오른쪽 클릭됨!');
const middleClick = () => alert('가운데 클릭됨!');
</script>
<template>
  <div class="child">
    <button @click.left="leftClick">왼쪽 클릭</button>
    <button @click.right="rightClick">오른쪽 클릭</button>
    <button @click.middle="middleClick">가운데 클릭</button>
  </div>
</template>

<style lang="scss" scoped></style>
```

### 키입력 관련

- .enter : Enter 키가 눌렸을 때 실행
- .tab : Tab 키
- .delete : Delete & Backspace 키
- .esc : Escape 키
- .space : Space 키
- .up : 화살표 위 키
- .down : 화살표 아래 키
- .left : 화살표 왼쪽 키
- .right : 화살표 오른쪽 키

```vue
<script setup>
const submit = () => alert('제출됨!');
const deleteItem = () => alert('삭제됨!');
const escClick = () => alert('esc 클릭됨!');
</script>
<template>
  <div class="child">
    Enter 키를 눌러 제출 : <input type="text" @keyup.enter="submit" /> <br />
    delete 키를 눌러 삭제 : <input type="text" @keyup.delete="deleteItem" /> <br />
    esc 키를 눌러 취소 : <input type="text" @keyup.esc="escClick" /> <br />
  </div>
</template>
```

### 시스템 관련

- .ctrl : Ctrl 키를 누른 상태에서만 실행
- .alt : Alt 키를 누른 상태에서만 실행
- .shift : Shift 키를 누른 상태에서만 실행
- .meta : Mac의 ⌘(Command) 또는 Windows의 ⊞(Windows)

```vue
<script setup>
const clear = () => alert('입력값 초기화!');
const doSomething = () => alert('Ctrl + 클릭 실행됨!');
const onClick = () => alert('클릭 됨');
const onCtrlClick = () => alert('ctrl + 클릭 됨');
</script>
<template>
  Alt+Enter 초기화 : <input @keyup.alt.enter="clear" /> <br />
  <button @click.ctrl="doSomething">Ctrl + 클릭 실행</button> <br />
  <button @click.ctrl.exact="onCtrlClick">Ctrl만 눌러야 실행됨</button> <br />
  <button @click.exact="onClick">다른 키 없이 클릭해야 실행됨</button> <br />
</template>
```

```toc

```
