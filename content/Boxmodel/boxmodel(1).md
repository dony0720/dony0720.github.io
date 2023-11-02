---
emoji: 🧢
title: Box model(1) - content,padding
date: '2023-03-28 16:00:00'
author: 중석 
tags: CSS 
categories: CSS  
---

# css box-model (1)

# box-model 

1. `box-model`이란?    
    + 모든 HTML의 요소는 box 모양으로 구성되어 있습니다. 
    
    + 박스모델은 content, padding, border, margin으로 구성되어 있습니다.

2. `box-model`구성요소 
    
    + `content` : 텍스트나 이미지를 포함하는 실질적인 내용을 포함하는 부분 
    
    + `padding` : content(내용)과 border(테두리) 사이에 위치하는 내부 여백 부분 
    
    + `border` : padding(패딩)과 margin(마진) 사이에 위치하는 테두리 부분 
    
    + `margin` : 가장 바깥쪽에 위치한 외부 여백 부분 

# width와 height 속성 

css에서 width와 height 속성을 설정할때에 가르키는 부분은 content(내용) 부분만을 가르킨다.    
다른 부분인 padding, border, margin은 포함되지 않는다. 

<br>
<br>

## width 속성 


```css
<style>

    div{
        text-align: center;
        background-color: aqua;
        }
    
</style>
```
```html
<body>
    <div>width</div>
</body>

```

+ 위의 코드를 실행해 보면 div태그의 길이가 body 전체의 길이를 갖는걸 볼 수 있다.

<br>

```css
<style>

    div{
        text-align: center;
        background-color: aqua;
        width: 50%;
        }
</style>
```
```html
<body>
    <div>width</div>
</body>

```

+ width에 50%의 값을 할당하게 되면 div 태그의 길이가 절반이 되는걸 볼 수 있다. 


## height 속성 


```css
<style>

    div{
        background-color: aqua;
        text-align: center;
        height: 50px;
        }
        
</style>
```
```html
<body>
   <div>width</div>
</body>

```

+ height에 50px 값을 할당해 높이의 변화가 생긴걸 알 수 있다, 


# padding 속성 

**css에서는 padding에 다음과 같은 속성을 제공합니다**   

1. padding-top 
    + padding의 위쪽 부분을 가리킴    

2. padding - right
    + padding의 오른쪽 부분을 가리킴    

3. padding - bottom 
    + padding의 아래쪽 부분을 가리킴    

4. padding - left
    + padding의 왼쪽 부분을 가리킴     

<br>
<br>

## padding의 개별 설정

**top, right, bottom, left의 padding 속성값을 한줄로 설정할때 사용합니다** 

<br>


## padding의 속성값이 4개일때 

**top, right, bottom, left의 순으로 값을 할당하게 된다**



```css
<style>

    div{
        background-color: aqua;
        text-align: center;
        padding: 20px 40px 60px 80px
        }
    
</style>
```
```html    
<body>
   <div> width</div>
</body>

```

**위 코드의 의미는 다음과 같다**

1. padding-top: 20px  

2. padding-right: 40px 

3. padding-bottom: 60px

4. padding-left: 80px  

<br>
<br> 

## padding의 속성값이 3개일때 

**top, right와 left, bottom의 순으로 값을 할당하게 된다**


```css
<style>

    div{
        background-color: aqua;
        text-align: center;
        padding: 20px 40px 60px
        }
    
</style>
```
```html    
<body>
   <div> width</div>
</body>

```

**위 코드의 의미는 다음과 같다**

1. padding-top: 20px  

2. padding-right: 40px 

3. padding-bottom: 60px

4. padding-left: 20px  

<br>
<br> 

## padding의 속성값이 2개일때 

**top와 bottom, right와 left의 순으로 값을 할당하게 된다**


```css
<style>

    div{
        background-color: aqua;
        text-align: center;
        padding: 20px 40px
        }
    
</style>
```
```html
<body>
   <div> width</div>
</body>

```

**위 코드의 의미는 다음과 같다**

1. padding-top: 20px  

2. padding-right: 40px 

3. padding-bottom: 20px

4. padding-left: 40px  

```toc

```