---
emoji: 🧢
title: Box model(2) - border
date: '2023-03-28 16:00:00'
author: Js 
tags: CSS 
categories: CSS  
---

# border 속성 


1. **css에서 border에 제공하는 속성은 다음과 같습니다** 

    + dotted: 테두리를 점선으로 설정합니다.

    + dashed: 테두리를 약간 긴 점선으로 설정합니다. 

    + solid: 테두리를 실선으로 설정합니다.

    + double: 테두리를 이중선으로 설정합니다. 

    + groove: 테두리를 3차원인 입체적인 선으로 border-color에 영향을 받습니다. 

    + ridge: 테두리를 3차원인 능선효과가 있는 선으로 설정하며 border-color에 영향을 받습니다. 

    + inset: 테두리를 3차원인 내지로 끼운 선으로 설정하며 border-color에 영향을 받습니다. 

    + outset: 테두리를 3차원인 외지로 끼운 선으로 설정하며 border-color에 영향을 받습니다. 

    + none: 테투리를 없앱니다.

    + hidden: 테투리는 존재하지만 보이지 표현하지 않습니다. 


```css
<style>

    .dotted{border: dotted red; margin: 20px;}

    .dashed{ border: dashed red; margin: 20px;}

    .solid{border: solid red;  margin: 20px;}

    .double{border: double red; margin: 20px;}

    .groove{border: groove red; margin: 20px;}

    .ridge{border: ridge red; margin: 20px;}

    .inset{border: inset red; margin: 20px;}

    .outset{border: outset red; margin: 20px;}
        
    .none{border: none; margin: 20px;}

    .hidden{border: hidden; margin: 20px;}
    
</style>

<body>

    <div class="dotted">dotted</div>
   
    <div class="dashed">dashed</div>
    
    <div class="solid">solid</div>
    
    <div class="double">double</div>
    
    <div class="groove">groove</div>
    
    <div class="ridge">ridge</div>
    
    <div class="inset">inset</div>
    
    <div class="outset">outset</div>
    
    <div class="none">none</div>
    
    <div class="hidden">hidden</div>
    
</body>
```


# border-width 속성 

1. **테두리의 두께를 설정합니다** 

2. **px, em, cm등과 같은 css 크기 단위를 이용해 두께를 직접 설정 할 수 있습니다** 

3. **미리 설정된 thin, medium, thick를 사용할 수 있습니다** 


```css
<style>

    .dotted-a{
        border-style: dotted red;
        border-width: 2px;
        margin: 20px;
    }

    .dotted-b{
        border-style: dotted red;
        border-width: 5px;
        margin: 20px;
    }

    .dashed-a{
        border-style: dashed red;
        border-width: thin;
        margin: 20px;
    }

    .dashed-b{
        border-style: dashed red;
        border-width: thick;
        margin: 20px;
    }

    .solid-a{
        border-style: solid red;
        border-width: 2px;
        margin: 20px;
    }

    .solid-b{
        border-style: solid red;
        border-width: thick;
        margin: 20px;
    }

    .mix {
       border-style:solid red;
       border-width: 2px thin 5px thick;
       margin: 20px;
    }
    
    </style>

<body>

    <div class="dotted-a">border-width: 2px</div>
    
    <div class="dotted-b">border-width: 5px</div>
    
    <div class="dashed-a">dashed에 border-width: thin</div>
    
    <div class="dashed-b">dashed에 border-width: thick</div>
    
    <div class="solid-a">solid에 border-width: 2px</div>
    
    <div class="solid-b">solid에 border-width: thick</div>
    
    <div class="mix">top: 2px; right: thin bottom: 5px; left:thick</div>

</body>
```


# border-color 

1. **테두리의 색상을 지정합니다** 

2. **기본적인 color 속성 외에 투명한 색을 지정하는 transparent 속성값도 사용가능합니다**
    
3. **색상을 지정할때는 아래와 같은 방법이 있습니다** 
    
    + border-color: red; 
    
    + border-color: rgb(0,0,255); 
       
       1) red, green, blue 순으로 0~255 사이에 값을 주어 색상 지정하고 
       
       2) 예시를 든 결과값은 blue 색상 
    
    + border-color: rgba(0,0,255,0.5);
    
        1) 앞3개의 인자는 2번과 같이 값을 할당하고 마지막인자는 투명도를 결정한다.
        
        2) 마지막인자에 0~1 사이의 값을 주어 투명도를 결정한다. 
    
    + border-color: #0000FF
        
       +  RGB의 16진수 값을 가져와 색상을 지정합니다 
     
    + border-color: #0000FF red blue green 
        
       + top, right, bottom, left 순으로 각각의 색상을 지정합니다
       
       
4. **border-color 속성값이 설정되지 않으면 해당 element의 color 속성값을 물려받습니다** 



```css
    <style>    
    
        .red{
            border:solid 5px;
            border-color: red; 
            margin: 20px;
        }

        
        .rgb{
            border: solid 5px;
            border-color: rgb(0,0,255); 
            margin: 20px;
        }
        
        .rgba{
            border: solid 5px;
            border-color: rgba(0,255,0,0.5); 
            margin: 20px;
        }
        
        .Hexadecimal{
            border: solid 5px;
            border-color: #0000FF;
            margin: 20px;
        }
        
        .Individual_Settings{
            border: solid 5px;
            border-color: #0000FF red aqua   green ;
            margin: 20px;
        }
       
        h4{
            border: solid ;
        }
        
    </style>

<body>
    
    <div class="red">border-color:red</div>
    
    <div class="rgb"> border-color: rgb(0,0,255)</div>
    
    <div class="rgba"> border-color: rgba(0,0,255,0.5); </div>
    
    <div class="Hexadecimal"> border-color: #0000FF</div>
    
    <div class="Individual_Settings">border-color: #0000FF red aqua green </div>
    
    <h4>boder속성 지정 안함 </h4>

</body>
```
![](https://github.com/dony0720/dony0720.github.io/blob/master/image/border-color%20%EC%86%8D%EC%84%B1.png) 

# border-style의 개별 설정 

## 속성이 4개일때 


```css
<style>
    .individual_Settings4{
        border-style: solid dashed dotted double;
        margin: 20px;
    }
</style>

<body>
    <div class="individual_Settings4">4개의 border-style 개별설정</div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. border-top-style: solid;

2. border-right-style: dashed;
   
3. border-bottom-style: dotted;   
   
4. border-left-style: double;

## 속성이 3개일때 


```css
<style>
    .individual_Settings3{
        border-style: solid dashed dotted;
        margin: 20px;
    }
</style> 

<body>
    <div class="individual_Settings3">3개의 border-style 개별설정</div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. border-top-style: solid;
   
2. border-right-style: dashed;
   
3. border-bottom-style: dotted;
      
4. border-left-style: dashed;
   


## 속성이 2개일때 


```css
<style>
    .individual_Settings2{
        border-style: dashed dotted;
        margin: 20px;
    }
</style> 

<body>
    <div class="individual_Settings2">2개의 border-style 개별설정</div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. border-top-style: dashed;
   
2. border-right-style: dotted;

3. border-bottom-style: dashed;
   
4. border-left-style: dotted;
   

## 속성이 1개일때 


```css
<style>
    .individual_Settings1{
        border-style: solid;
        margin: 20px;
    }
</style> 

<body>
    <div class="individual_Settings1">1개의 border-style 개별설정</div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. border-top-style: solid;
   
2. border-right-style: solid;

3. border-bottom-style: solid;
   
4. border-left-style: solid;
   
<br>
<br>
# border의 축약표현 


```css
<style>
   .good{
        border: dashed red 5px ;
        margin: 20px;
    }
</style>

<body>
    <div class="good">border의 축약표현</div>
</body>

```

**다음과 같이 모든 border 속성을 이용해서 한줄에 정의할 수 있다** 

![](https://github.com/dony0720/dony0720.github.io/blob/master/image/border%20%EC%B6%95%EC%95%BD%ED%91%9C%ED%98%84.png) 

# border-radius 속성 

1. **모든 HTML 요소에 border-radius 속성을 설정하여 모서리를 둥글게 만들 수 있다.**

2. **border-raidus 속성은 아래 네 가지 속성의 스타일을 한 줄에 설정한 것이다** 

    + border-top-left-radius 
    
    + border-top-right-radius 
    
    + border-bottom-right-radius 
    
    + border-bottom-left-radius 

# border-radius의 개별 설정 

## 속성이 4개일때 


```css
<style>
    .individual_Settings4{
        border-radius: 20px 40px 60px 80px;
    }
</style>

<body>
    <div class="individual_Settings4">border-radius 속성 4개 </div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. border-radius-top-left: 20px

2. border-radius-top-right: 40px 

3. border-radius-bottom-right: 60px 

4. border-radius-bottom-left: 80px 

## 속성이 3개일때 


```css
<style>
    .individual_Settings3{
        border-radius: 20px 40px 80px;
    }
</style>

<body>
    <div class="individual_Settings3">border-radius 속성 3개 </div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. border-radius-top-left: 20px

2. border-radius-top-right: 40px 

3. border-radius-bottom-right: 80px 

4. border-radius-bottom-left: 40px 

## 속성이 2개일때


```css
<style>
    .individual_Settings2{
        border-radius: 20px 80px;
    }
</style>

<body>
    <div class="individual_Settings2">border-radius 속성 2개 </div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. border-radius-top-left: 20px

2. border-radius-top-right: 40px 

3. border-radius-bottom-right: 20px 

4. border-radius-bottom-left: 40px 

```toc

```