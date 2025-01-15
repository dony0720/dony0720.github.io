---
emoji: 👨🏻‍💻
title: Day 34 Styled-Components, Tailwind CSS
date: '2025-01-13 22:00:00'
author: 중석
tags: 프로그래머스
categories: 프로그래머스
---

# Styled-Components

Styled-Components는 CSS-in-JS 라이브러리 중 하나로, React 컴포넌트 내부에서 CSS를 작성할 수 있다. 스타일과 컴포넌트를 함께 정의하여 컴포넌트 단위로 관리할 수 있고, CSS 클래스 충돌을 방지하며 동적 스타일링이 가능하다.

## 기본 문법

```js
import styled from 'styled-components';

// Styled 컴포넌트 정의
const MyButton = styled.button`
  background-color: blue;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  &:hover {
    background-color: darkblue;
  }
`;

export default function Button({ children }) {
  return <MyButton>{children}</MyButton>;
}
```

## 동적 스타일링

```js
const Button = styled.button`
  background-color: ${(props) => (props.primary ? 'blue' : 'gray')};
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
`;

export default function App() {
  return (
    <div>
      <Button primary>Primary 버튼</Button>
      <Button>Secondary 버튼</Button>
    </div>
  );
}
```

## 컴포넌트 상속

```js
const Button = styled.button`
  background-color: gray;
  color: white;
  padding: 10px 20px;
`;

const PrimaryButton = styled(Button)`
  background-color: blue;
`;

export default function App() {
  return (
    <div>
      <Button>기본 버튼</Button>
      <PrimaryButton>Primary 버튼</PrimaryButton>
    </div>
  );
}
```

## 중첩 스타일링

```js
const Card = styled.div`
  background: white;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 20px;

  h1 {
    font-size: 24px;
    margin-bottom: 10px;
  }

  p {
    color: gray;
    font-size: 14px;
  }
`;

function App() {
  return (
    <Card>
      <h1>카드 제목</h1>
      <p>카드 내용</p>
    </Card>
  );
}
```

# Tailwind CSS

Tailwind CSS는 오픈 소스 CSS 프레임워크로, 각 요소를 스타일링하기 위해 조합하여 사용할 수 있는 "유틸리티" CSS 클래스 목록을 제공한다.

## Tailwind CSS 특징

1. 유틸리티 클래스 기반 스타일링

- Tailwind는 bg-blue-500, text-lg, p-4 등과 같이 단일 CSS 속성을 나타내는 유틸리티 클래스를 제공한다. 이를 조합하여 원하는 디자인을 구현할 수 있으며, 별도의 CSS 파일을 작성하지 않고도 HTML 내에서 직접 스타일링이 가능하다.

2. 반응형 디자인 지원

- sm:, md:, lg:, xl: 등의 프리픽스를 사용하여 다양한 화면 크기에 따라 스타일을 조정할 수 있어, 반응형 웹 디자인을 손쉽게 구현할 수 있다.

3. 상태 기반 스타일링

- hover:, focus:, active: 등의 프리픽스를 통해 사용자 상호작용에 따른 상태 기반 스타일링이 가능하다.

4. 커스터마이징 및 확장성

- tailwind.config.js 파일을 통해 색상, 폰트, 간격 등 다양한 디자인 요소를 손쉽게 커스터마이징할 수 있으며, 프로젝트 요구에 맞게 유틸리티 클래스를 추가하거나 수정하여 유연하게 확장할 수 있다.

```toc

```
