---
emoji: 👨🏻‍💻
title: Day 56 Vue Style & class 적용
date: '2025-02-17 23:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 기본적인 class 기반 css 적용 방법

- style scoped 해당 컴포넌트 내부에서만 스타일이 적용되도록 제한하는 기능이다.
- 내부적으로 고유한 데이터 속성을 추가하여 CSS 선택자를 스코프 내에서만 유효하도록 만든다.
- 단, 자식 컴포넌트에는 스타일이 상속되지 않는다.
- style을 활용하면 전역 CSS가 적용되지만 일반적으로 .css를 활용 추천

## class 바인딩 (ref)

```vue
<script setup>
import { ref } from 'vue';

const isActive = ref(true);
const hasError = ref(true);
</script>

<template>
  <div class="child">
    <div class="basic" v-bind:class="{ active: isActive }">클래스 바인딩 컴포넌트1</div>

    <div class="basic" :class="{ active: isActive, error: hasError }">클래스 바인딩 컴포넌트2</div>

    <div :class="{ basic: true, active: isActive, error: hasError }">클래스 바인딩 컴포넌트3</div>

    <label>isActive : <input type="checkbox" v-model="isActive" /></label> <br />
    <label>hasError : <input type="checkbox" v-model="hasError" /></label>
  </div>
</template>

<style scoped>
.basic {
  border: 1px solid black;
}

.active {
  color: blue;
}

.error {
  text-decoration: line-through;
}
</style>
```

## class 바인딩 (reactive)

```vue
<script setup>
import { reactive } from 'vue';
const classObject = reactive({
  active: true,
  error: false,
});
</script>

<template>
  <div class="child">
    <div class="basic" v-bind:class="classObject">클래스 바인딩 컴포넌트1</div>

    <div class="basic" :class="classObject">클래스 바인딩 컴포넌트2</div>

    <label>isActive : <input type="checkbox" v-model="classObject.active" /></label> <br />
    <label>hasError : <input type="checkbox" v-model="classObject.error" /></label>
  </div>
</template>

<style scoped>
.basic {
  border: 1px solid black;
}

.active {
  color: blue;
}

.error {
  text-decoration: line-through;
}
</style>
```

## class 바인딩 (이벤트 적용)

```vue
<script setup>
import { reactive } from 'vue';

const style1 = reactive({ backgroundColor: 'white', color: 'black' });

const overEvent = () => {
  style1.backgroundColor = 'purple';
  style1.color = 'yellow';
};

const outEvent = () => {
  style1.backgroundColor = 'aqua';
  style1.color = 'black';
};
</script>

<template>
  <div class="child">
    <button :style="style1" @mouseover.stop="overEvent" @mouseout="outEvent">테스트</button>
  </div>
</template>
```

# class 기반 동적 바인딩

## v-bind 기반 class 연동 문법(문자열로 관리)

- ':class'를 활용하여 미리 정의된 class를 지정할 수 있다.

```vue
<script setup>
import { ref } from 'vue';

// class 이름을 문자열로 관리하는 방법
const myButtonStyle = ref('buttonColor buttonLayout');
</script>

<template>
  <div class="child">
    <button class="staticBorder" :class="myButtonStyle">테스트 버튼</button>
  </div>
</template>

<style scoped>
.buttonColor {
  background-color: aqua;
  color: black;
}
.buttonLayout {
  text-align: center;
  width: 120px;
}
.staticBorder {
  border: blue dashed 3px;
}
</style>
```

## v-bind 기반 class를 여러 개로 적용하는 방법(배열 관리)

- `:class` 속성에 `[]` 리스트를 통해 여러 속성을 한 번에 적용할 수 있다

```vue
<script setup>
import { ref } from 'vue';

const myColor = ref('buttonColor');
const myLayout = ref('buttonLayout');
</script>

<template>
  <div class="child">
    <button class="staticBorder" :class="[myColor, myLayout]">테스트 버튼</button>
  </div>
</template>

<style scoped>
.buttonColor {
  background-color: aqua;
  color: black;
}
.buttonLayout {
  text-align: center;
  width: 120px;
}
.staticBorder {
  border: blue dashed 3px;
}
</style>
```

## 삼항 연산자, 논리 연산자

- 삼항 연산자를 통해 레이아웃 속성을 여러 레이아웃으로 대체할 수 있다.
- 삼항 연산자 대신 논리 연산자 `&& || `를 통해 단축해서도 표현할 수 있다.

```vue
<script setup>
import { ref } from 'vue';

const myColor = ref('buttonColor');
const myLayout = ref('buttonLayout');
const myShadow = ref('buttonShadow');
const isMyLayout = ref(false);
</script>

<template>
  <div class="child">
    <button
      class="staticBorder"
      :class="[myColor, isMyLayout ? myLayout : '', isMyLayout && myShadow]"
    >
      테스트 버튼
    </button>
    <hr />
    <label>
      레이아웃 적용 여부
      <input type="checkbox" v-model="isMyLayout" />
    </label>
  </div>
</template>

<style scoped>
.buttonColor {
  background-color: aqua;
  color: black;
}
.buttonLayout {
  text-align: center;
  width: 150px;
}
.buttonShadow {
  box-shadow: 5px 5px #333;
}
.staticBorder {
  border: blue dashed 3px;
}
</style>
```

## v-model 기반 양방향 레이아웃 적용

```vue
<script setup>
import { ref } from 'vue';

const setColor = ref(false);
const setAlign = ref(false);
const setBorder = ref(false);
</script>

<template>
  <div class="child">
    <button :class="{ bColor: setColor, bLayout: setAlign, bBorder: setBorder }">버튼1</button>
    <div>
      <input type="checkbox" v-model="setColor" /> 색상
      <br />
      <input type="checkbox" v-model="setAlign" /> 정렬, 크기
      <br />
      <input type="checkbox" v-model="setBorder" /> 테두리 선
      <br />
    </div>
  </div>
</template>

<style scoped>
.bColor {
  background-color: aqua;
  color: black;
}

.bLayout {
  text-align: center;
  width: 120px;
}

.bBorder {
  border: blue dashed 3px;
}
</style>
```

## computed 기반 css 적용 방법

- v-model로 적용된 변수값에 따라 computed 메서드를 기반으로 처리할 수 있다.
- 이때의 장점은 메소드로 호출할 때 대비 계산량이 줄어든다.

```vue
<script setup>
import { computed, ref } from 'vue';

const score = ref(50);

const info = computed(() => ({
  warning: score.value < 1 || score.value > 100,
}));
</script>

<template>
  <div class="child">
    <b>1부터 100까지만 입력 가능합니다.</b><br />
    점수 : <input type="text" class="score" v-model.number.trim="score" :class="info" />
    <img
      src="https://contactsvc.bmaster.kro.kr/img/error.png"
      v-if="info.warning"
      class="warnimage"
    />
    <br />
    <br />
    입력된 점수 : {{ score }}
  </div>
</template>

<style scoped>
.score {
  border: solid 1px black;
}

.warning {
  margin-left: 3px;
  background-color: yellow;
  color: purple;
}

.warnimage {
  width: 18px;
  height: 18px;
  top: 5px;
  position: relative;
}
</style>
```

```toc

```
