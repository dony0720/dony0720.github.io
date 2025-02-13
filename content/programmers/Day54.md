---
emoji: 👨🏻‍💻
title: Day 54 Vue 반응형 API
date: '2025-02-13 23:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# 반응형 API (Reactivity API)

1. 반응형 API (Reactivity API)는 데이터의 변경을 자동으로 감지하고, UI를 최신 상태로 유지하는 API이다.
2. 기본적으로 Vue는 데이터가 변경되면 자동으로 DOM을 업데이트하는데, 이를 가능하게 하는 핵심
   개념이 반응형 시스템(Reactivity System)이다.
3. React의 Hooks와 유사한 개념으로 useState를 ref, reactive로 useEffect는 watch와 watchEffect가 대응

## ref

1. ref()는 기본 데이터 타입(Number, String, Boolean, Object, Array 등)을 반응형으로 만드는 API 이다.
2. 기본형을 감싸서(Wrapping)하여 관리함에 따라 .value 속성을 통해 값을 읽고 수정이 가능하다.
3. 객체를 ref로 감싸면 내부적으로 reactive()와 유사하게 동작하며, reactive 다르게 ref로는 null로 초기화
   가능하고 객체로 할당하는 경우 reactive를 통해 깊숙이(deeply) 반응함으로 속성값 변경도 감지 된다.
4. 간혹, deep 하게 감지 되지 않는 경우도 존재한다. watch 결합과 같은 경우, 이때는 deep 옵션 활용 필수다

### 기본형 예제

```vue
<script setup>
import { ref } from 'vue';

const count = ref(0);
const message = ref('');
const number = ref(3);
const isChecked = ref(false);

const increment = () => {
  count.value++;
};
</script>

<template>
  카운트 : {{ count }} <br />
  <button @click="increment">증가</button> <br /><br />

  입력한 메시지 :{{ message }} <br />
  <input type="text" name="" id="" v-model="message" placeholder="메세지를 입력바랍니다" /> <br />
  <br />

  입력한 숫자 : {{ number * 10 }} <br />
  <input type="text" name="" id="" v-model="number" placeholder="숫자를 입력하세요" /> <br />
  <br />

  체크 상태 : {{ isChecked }} <br />

  <input type="checkbox" name="" id="" v-model="isChecked" /> <br />
  <br />
</template>
```

### 객체 예제

```vue
<script setup>
import { onMounted, ref } from 'vue';

// 객체 선언
const user = ref(null);

// 배열 선언
const languages = ref(['C', 'Java', 'JavaScript']);

onMounted(() => {
  // axios로 데이터 받아오는 곳
  setTimeout(() => {
    user.value = { name: '홍길동', age: '25', favoriteLanguage: 'Java' };
  }, 3000);
});
</script>

<template>
  <template v-if="user">
    <h3>사용자 정보 입력</h3>
    이름 : <input type="text" v-model="user.name" /> <br />
    나이 : <input type="number" v-model="user.age" /> <br />
    좋아하는 언어 :
    <select v-model="user.favoriteLanguage">
      <option v-for="item in languages" :key="item" :value="item">{{ item }}</option>
    </select>

    <h3>입력한 정보</h3>
    이름 : {{ user.name }} <br />
    나이 : {{ user.age }} <br />
    좋아하는 언어 : {{ user.favoriteLanguage }} <br />
  </template>
  <template v-else>
    <h3>로딩중...</h3>
  </template>
</template>
```

- onMounted에 의해 Dom이 마운트 된 후에 setTimeout이 동작된다.
- 처음 렌더링 시에는 로딩중으로 나오게 된다.
- setTimeout 함수가 3초 지난후에는 user의 값이 바뀌어 재렌더링이 된다.

## reactive

1. reactive()는 객체(Object)와 배열(Array) 를 반응형 상태로 만드는 API이다.
2. ref와 달리 Wrapping 하지 않고 반응형 프록시(proxy, 변경을 감지하는 JS 패턴)를 활용, .value를 사용하지 않고 속성에 직접 접근이 가능하다.
3. ref()와 달리 기본 타입은 사용할 수 없고, 객체나 배열만 가능하며, null로 초기화 될 수 없다.
4. Deep(깊은 복사) 동작함으로 ref에서 객체로 활용 할 때 이슈가 있으면 reactive를 활용 권장한다고 한다.

### 객체 예제

```vue
<script setup>
import { onMounted, reactive, ref } from 'vue';

const isLoading = ref(true);
const user = reactive({ name: '홍길동', age: 25, favoriteLanguage: 'JavaScript' });
const languages = reactive(['C', 'Java', 'JavaScript']);

onMounted(() => {
  setTimeout(() => {
    const newUser = { name: '홍길동', age: 25, favoriteLanguage: 'Java' };

    // 속성 직접 접근
    user.name = newUser.name;
    user.age = newUser.age;
    user.favoriteLanguage = newUser.favoriteLanguage;
    isLoading.value = false;
  }, 3000);
});
</script>

<template>
  <h3>사용자 정보 입력</h3>
  이름 : <input v-model="user.name" type="text" /> <br />
  나이 : <input v-model="user.age" type="number" /> <br />
  좋아하는 언어:
  <select v-model="user.favoriteLanguage" class="input">
    <option v-for="lang in languages" :key="lang" :value="lang">
      {{ lang }}
    </option>
  </select>
  <br />

  <h3>입력한 정보</h3>
  이름: {{ user.name }}<br />
  나이: {{ user.age }}<br />
  좋아하는 언어: {{ user.favoriteLanguage }}<br />
</template>
```

## computed( ) - 반응형 재계산

1. computed()는 기존 데이터(state)를 기반으로 새로운 값을 자동 계산하는 API이다.
2. 종속된 값이 변경되면 자동으로 재계산 되며, 읽기 전용으로 활용한다. (기본적으로 읽기 전용이지만, set을 지원하기도 한다.)
3. react의 useMemo와 유사한 방법으로 함수 내부의 값들이 변경되면 자동으로 계산되는 기능이라고 한다.

### 기본형 예제

```vue
<script setup>
import { computed, ref } from 'vue';

const price = ref(1000);
const quantity = ref(2);

// 자동으로 계산되는 속성
const totalPrice = computed(() => price.value * quantity.value);
</script>

<template>
  <h3>물품 가격</h3>
  가격 : <input type="text" name="" id="" v-model="price" /> 원 <br />
  수량 : <input type="text" name="" id="" v-model="quantity" /> 개 <br />
  <b>총 가격 : {{ totalPrice }} 원</b>
</template>
```

### get / setter 예제

```vue
<script setup>
import { computed, ref } from 'vue';

const firstName = ref('John');
const lastName = ref('Doe');

const fullName = computed({
  // getter
  get() {
    return firstName.value + ` ` + lastName.value;
  },

  //setter
  set(newValue) {
    if (newValue.includes(' ')) {
      [firstName.value, lastName.value] = newValue.split(' ');
    }
  },
});
</script>

<template>
  <div>
    firstName : <input type="text" name="" id="" v-model="firstName" /> <br />
    lastName : <input type="text" name="" id="" v-model="lastName" /> <br />
    fullName: <input type="text" name="" id="" v-model="fullName" /> <br />
    fullName: {{ fullName }} <br />
  </div>
</template>
```

- Getter
  firstName과 lastName을 공백(" ")으로 연결하여 fullName을 반환한다. (예: "John Doe")

- Setter
  새로운 fullName 값이 입력되었을 때, 공백이 포함된 경우 split(' ')을 사용하여 firstName과 lastName을 각각 나눈다. (예: "John Doe" → firstName = "John", lastName = "Doe")

## watch() - 데이터 변경 감지

1. watch( )는 특정 데이터의 변화를 감지하는 API
2. 보통 변경을 감지하고 특정 로직 (예: API 호출, 상태 업데이트, 콘솔 로그, 알림 등) 을 실행한다.
3. computed( )는 결과값을 반환하지만, watch()는 반응형 데이터를 변경했을 때 특정 동작을 실행 한다.
4. ref 객체나 배열 조합시에는 반드시 { deep: true } 옵션이 필수다.

### watch - 기본형 예제(데이터 1개 감시)

```vue
<script setup>
import { ref, watch } from 'vue';

const count = ref(0);
const logs = ref([]);

// 기본
// watch(count, () => {
//   logs.value.push(count.value)
// })

// 신규값만 가져오는 방법
// watch(count, (newValue) => {
//   logs.value.push(newValue)
// })

// 3. new + old 값 가져오기 => 현재 값, 이전 값
watch(count, (newValue, oldValue) => {
  console.log(`count 변경: ${oldValue} → ${newValue}`);
  logs.value.push(`count 변경: ${oldValue} → ${newValue}`);
});

const increment = () => {
  count.value++;
};

const decrement = () => {
  count.value--;
};
</script>

<template>
  <div>
    count : {{ count }} <br />
    <button @click="increment">증가</button>
    <button @click="decrement">감소</button>
    <div v-for="item in logs" :key="item">{{ item }}</div>
  </div>
</template>
```

### watch - 기본형 예제(데이터 2개 이상 감시)

```vue
<script setup>
import { ref, watch } from 'vue';

const price = ref(1000);
const quantity = ref(2);
const totalPrice = ref(price.value * quantity.value);
const logs = ref([]);

// 자동으로 계산되는 속성
// const totalPrice = computed(() => price.value * quantity.value)

// watch 처리
// 1. 여러개 기본형
watch([price, quantity], () => {
  totalPrice.value = price.value * quantity.value;
  logs.value.push(`${price.value}, ${quantity.value}`);
});
</script>

<template>
  <h3>물품 가격</h3>
  가격 : <input type="text" name="" id="" v-model="price" /> 원 <br />
  수량 : <input type="text" name="" id="" v-model="quantity" /> 개 <br />

  <b>총 가격 : {{ totalPrice }} 원</b>

  <div v-for="item in logs" :key="item">{{ item }}</div>
</template>
```

- price, quantity 둘 중에 하나의 값이라도 변경되면 해당 로직을 실행한다.

## watchEffect() - 자동 감지 및 실행

1. watchEffect()는 내부에서 사용된 모든 반응형 상태를 자동으로 감지하는 API이다.
2. watch()와 달리 어떤 변수를 감시할지 명시할 필요 없으나 모든 변수의 변화를 감지하여 동작한다.
3. 이전 값에 대한 모니터링이 불가능하다

### watchEffect - 기본형 예제

```vue
<script setup>
import { ref, watch, watchEffect } from 'vue';

const count = ref(0);
const logs = ref([]);

watchEffect(() => {
  logs.value.push(`count 변경 : ${count.value}`);
});

const increment = () => {
  count.value++;
};

const decrement = () => {
  count.value--;
};
</script>

<template>
  <p>카운트: {{ count }}</p>
  <button @click="increment">증가</button>
  <button @click="decrement">감소</button>
  <div v-for="item in logs" v-bind:key="item">
    {{ item }}
  </div>
</template>
```

```toc

```
