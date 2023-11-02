---
emoji: 🧢
title: TodoList (10) - Quote 자동 생성기
date: '2023-03-29 16:30:00'
author: 중석 
tags: TodoList 작성 
categories: Js 
---
# Quote 생성

## 소스코드 


```js
const quotes = [
  {
    quote: `The way to get started is to quit talking and begin doing.`,
    author: "Walt Disney",
  },
  {
    quote: `Life is what happens when you're busy making other plans.`,
    author: "John Lennon",
  },
  {
    quote:
      `The world is a book and those who do not travel read only one page.`,
    author: "Saint Augustine",
  },
  {
    quote: `Life is either a daring adventure or nothing at all.`,
    author: "Helen Keller",
  },
  {
    quote: `To Travel is to Live`,
    author: "Hans Christian Andersen",
  },
  {
    quote: `Only a life lived for others is a life worthwhile.`,
    author: "Albert Einstein",
  },
  {
    quote: `You only live once, but if you do it right, once is enough.`,
    author: "Mae West",
  },
  {
    quote: `Never go on trips with anyone you do ntot love.`,
    author: "Hemmingway",
  },
  {
    quote: `We wander for distraction, but we travel for fulfilment.`,
    author: "Hilaire Belloc",
  },
  {
    quote: `Travel expands the mind and fills the gap.`,
    author: "Sheda Savage",
  },
];

const quote = document.querySelector(".quote-box div:nth-child(2)"); 
//element:nth-child(a) a에 원하는 순서(위->아래)의 번호를 넣어 자식을 선택 

const author = document.querySelector(".quote-box div:last-child");
const quoteBox = document.querySelector(".quote-box")
const todaysQuote = quotes[Math.floor(Math.random() * quotes.length)];

quote.innerText = todaysQuote.quote;
author.innerText = `-${todaysQuote.author}-`;


function changeQuoute() {
  const todaysQuote = quotes[Math.floor(Math.random() * quotes.length)];
  quote.innerText = todaysQuote.quote;
  author.innerText = `-${todaysQuote.author}-`;
  console.log(1);
}

quoteBox.addEventListener("click", changeQuoute)


```

## changeQuoute 함수 


```js
const todaysQuote = quotes[Math.floor(Math.random() * quotes.length)];
quote.innerText = todaysQuote.quote;
author.innerText = `-${todaysQuote.author}-`;
```

1. **const todaysQuote = quotes[Math.floor(Math.random() * quotes.length)]**

    + 0~1사이에 난수를 생성는 **Math.random**을 사용    
    
    + 발생한 난수를 quotes 배열의 길이 만큼 곱해 **0 ~ quotes.length** 사이에 난수를 생성
    
    + Math.floor를 사용해 소수점 뒷자리를 반올림해 정수를 생성  


```toc

```