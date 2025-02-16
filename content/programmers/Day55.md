---
emoji: 👨🏻‍💻
title: Day 55 Vue 컴포넌트 연동
date: '2025-02-14 23:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 컴포넌트 연동

Vue 컴포넌트 연동에 핵심이 되는 3가지 개념은 props, emit 그리고 v-model이 있다.

- props : 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 Read-Only 속성, defineProps() 사용
- emit : 자식 컴포넌트에서 부모 컴포넌트로 이벤트를 전달하는 방법, defineEmits(), $emit() 사용
- v-model : 부모와 자식 간의 양방향 바인딩으로 props + emit을 합친 개념, defineModel() 사용

## props

- Props는 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 방법
- defineProps를 통해 자식 컴포넌트에서 부모에서 받을 props를 정의
- html 속성 처럼 camelCase가 아닌 kebab-case로 이름을 정의하는 것을 권장 (greeting-message="안녕!")
- 단방향 데이터 흐름을 유지해야 하며, props로 받은 값은 자식에서 직접 수정할 수 없다. (read only)
- 단방향 데이터 흐름일지라도 부모에서 props를 변경하면 이를 감지하여 자동으로 업데이트 된다.

### 예제 1

```vue
// 부모 컴포넌트
<script setup>
import ChildComponent1 from './ChildComponent1.vue';
</script>

<template>
  <div>
    <h3>Parent Component1</h3>
    <ChildComponent1 title="Vue의 Props" :count="10" />
  </div>
</template>

// 자식 컴포넌트
<script setup>
// props 선언부

// props를 js에서 활용할 일이 있으면 props를 선언하여 받는다.
const props = defineProps({
  title: String,
  count: Number,
});

console.log(props.count);
console.log(props.title);
</script>

<template>
  <div class="child">
    <b>{{ title }}</b
    ><br />
    Count: {{ count }}<br />
  </div>
</template>
```

### 예제 2

```vue
// 부모 컴포넌트 (Parent Component2)

<script setup>
import ChildComponent2 from './ChildComponent2.vue';

const title = 'Vue Props 예제입니다.';
const count = 10;
const active = true;
const items = ['Apple', 'Banana', 'Cherry'];
const user = { name: 'Alice', age: 25 };
const today = new Date();
const callback = () => alert('Callback function!');
</script>

<template>
  <ChildComponent2
    :title="title"
    :count="count"
    :active="active"
    :items="items"
    :user="user"
    :today="today"
    :callback="callback"
  />
</template>

// 자식 컴포넌트 (ChildComponent2)
<script setup>
defineProps({
  title: String, // 문자열
  count: Number, // 숫자
  active: Boolean, // 불리언
  items: Array, // 배열
  user: Object, // 객체
  callback: Function, // 함수
  today: Date,
});
</script>

<template>
  <div class="child">
    <h3>{{ title }}</h3>
    count : {{ count }} <br />
    active : {{ active ? 'Y' : 'N' }} <br />
    item : <template v-for="(item, index) in items" :key="index">{{ item }},</template> <br />
    user : {{ user.name }}, {{ user.age }}<br />
    today : {{ today.toLocaleString() }}<br />
    <button @click="callback">callback</button>
  </div>
</template>
```

### 유효성 검사

```vue
// 부모 컴포넌트 (Parent Component3)
<script setup>
import ChildComponent3 from './ChildComponent3.vue';
</script>

<template>
  <ChildComponent3
    :prop-a="10"
    prop-b="Hello World"
    prop-c="required"
    :prop-d="null"
    prop-g="성공"
  />
</template>

// 자식 컴포넌트 (ChildComponent3)
<script setup>
defineProps({
  // 기본 타입 검사 (null, undefined 허용)
  propA: Number,
  // 여러 가지 가능한 타입
  propB: [String, Number],
  // 필수 문자열
  propC: {
    type: String,
    required: true,
  },
  // 필수이지만 널 허용 문자열
  propD: {
    type: [String, null],
    required: true,
  },
  // 기본값이 있는 숫자
  propE: {
    type: Number,
    default: 100,
  },
  propG: {
    validator(value) {
      // 값은 이 문자열 중 하나와 일치해야 합니다
      return ['성공', '경고', '위험'].includes(value);
    },
  },
});
</script>

<template>
  <div class="child">
    <h2>Child Component</h2>
    propA (Number): {{ propA }} <br />
    propB (String or Number): {{ propB }} <br />
    propC (Required String): {{ propC }} <br />
    propD (Required String or Null): {{ propD }} <br />
    propE (Number with Default 100): {{ propE }} <br />
    propG ('성공', '경고', '위험'): {{ propG }} <br />
  </div>
</template>
```

## emit

- Vue의 emit은 자식 컴포넌트에서 부모 컴포넌트로 이벤트를 전달하는 메커니즘이다.
- Vue3에서 도입된 $emit을 기반으로 활용하는 문법으로 단축된 emit 활용을 지원한다.
- 부모에서는 @some-event와 같이 kebab-case로 선언하고, 자식에는 camelCase로 호출하여도 문제없다.
- 또한 vue2 부터 활용하던 emit 패턴으로 defineEmits을 통해 emit을 활용하는 방법도 존재

### emit 기본 예제

```vue
// 부모 컴포넌트
<script setup>
import EmitBasic1 from './EmitBasic1.vue';

const handleSomeEvent = () => {
  alert('call handleSomeEvent');
  console.log('call handleSomeEvent');
};
</script>

<template>
  <EmitBasic1 @some-event="handleSomeEvent" />
</template>

// 자식 컴포넌트

<script setup></script>

<template>
  <div class="child">
    <h3>Child</h3>
    <!-- someEvent : 부모에서 정의 이벤트의 이름 -->
    <button @click="$emit('someEvent')">Click me</button>
  </div>
</template>
```

### 데이터 전달 예제 - emit

```vue
// 부모 컴포넌트
<script setup>
import EmitData1 from './EmitData1.vue';

const handleSomeEvent = (count, text) => {
  alert(`전달 된 데이터 : ${count}, ${text}`);
  console.log(`전달 된 데이터 : ${count}, ${text}`);
};
</script>

<template>
  <EmitData1 @some-event="handleSomeEvent" />
</template>

// 자식 컴포넌트
<script setup>
import { ref } from 'vue';

const count = ref(100);
const text = ref('안녕하세요?');
</script>

<template>
  <div class="child">
    <h3>Child</h3>
    count : <input type="text" v-model="count" /> <br />
    text : <input type="text" v-model="text" /> <br />

    <button @click="$emit('someEvent', count, text)">emit</button>
  </div>
</template>
```

### 데이터 전달 예제 - defineEmits

```vue
// 부모 컴포넌트

<script setup>
import EmitBasic2 from './EmitBasic2.vue';

const handleSomeEvent = () => {
  alert('call handleSomeEvent');
  console.log('call handleSomeEvent');
};
</script>

<template>
  <EmitBasic2 @some-event="handleSomeEvent" />
</template>

// 자식 컴포넌트
<script setup>
import { defineEmits } from 'vue';

// 이벤트 정의
const emit = defineEmits(['someEvent']);

const handleClick = () => {
  emit('someEvent');
};
</script>

<template>
  <div class="child">
    <h3>Child</h3>
    <button @click="handleClick">Click me</button>
  </div>
</template>
```

## v-model - defineModel()

- v-model을 컴포넌트에서 사용하여 양방향 바인딩을 구현할 수 있다.
- 또한 named를 붙여 하나가 아닌 여러 개의 v-model을 활용할 수 있다.
- Vue 3.4부터는 defineModel() 매크로를 사용하는 것을 권장한다.

### 다수의 v-model 활용

```vue
// 부모 컴포넌트
<script setup>
import { ref } from 'vue';
import ChildComponent2 from './ChildComponent2.vue';

const count = ref(0);
const text = ref('');
</script>

<template>
  <div>
    count : {{ count }} <br />
    text : {{ text }} <br />
    <ChildComponent2 v-model:count="count" v-model:text="text" />
  </div>
</template>

// 자식 컴포넌트 (ChildComponent2)

<script setup>
const count = defineModel('count');
const text = defineModel('text');

const increment = () => {
  count.value++;
};
</script>

<template>
  <div class="child">
    부모 count : {{ count }} <button @click="increment">click</button><br />
    <input type="text" v-model="text" />
  </div>
</template>
```

## Provide / Inject (전역 속성 공유)

- vue에서 props 없이 컴포넌트 간 데이터를 공유하는 방법 제공한다.
- provide()를 사용하여 부모가 값을 제공하고, inject()를 사용하여 자식이 값을 사용한다.
- provide(): 부모 컴포넌트에서 데이터를 제공 하는 메소드

### 반응형 예제

```vue
// 부모 컴포넌트
<script setup>
import { provide, ref } from 'vue';
import ChildComponent2A from './ChildComponent2A.vue';
import ChildComponent2B from './ChildComponent2B.vue';

const location = ref('북극');

const updateLocation = (newLocation) => {
  location.value = newLocation;
};

// provide를 통해 자식 컴포넌트에 값과 update 함수 제공
provide('location', { location, updateLocation });
</script>

<template>
  <div>
    <h3>부모 컴포넌트</h3>
    현재 위치 : {{ location }} <br />
    <ChildComponent2A />
    <ChildComponent2B />
  </div>
</template>

// 자식 컴포넌트 (ChildComponent2A)
<script setup>
import { inject } from 'vue';

// 부모에서 전달한 location과 update함수 선언
const { location, updateLocation } = inject('location');
</script>

<template>
  <div class="child">
    <h3>자식 컴포넌트 2A</h3>
    현재 위치 : {{ location }} <br />
    <button @click="updateLocation('남극')">남극 변경</button>
  </div>
</template>

// 자식 컴포넌트 (ChildComponent2B)

<script setup>
import { inject } from 'vue';

// 부모에서 전달한 location과 update함수 선언
const { location, updateLocation } = inject('location');
</script>

<template>
  <div class="child">
    <h3>자식 컴포넌트 2B</h3>
    현재 위치 : {{ location }} <br />
    <button @click="updateLocation('북극')">북극 변경</button>
  </div>
</template>
```

```toc

```
