---
emoji: 📝
title: Js_mission 
date: '2023-05-15 15:30:00'
author: Js 
tags: Mission 
categories: Mission  
---

# 필수 구현 사항 
+ function style의 문법을 사용해주세요.   

+ new 키워드를 통해 생성해서 사용됩니다.   

+ 파라메터로 아래와 같은 형태의 data를 넘겨받습니다. 

```
const data = [
  {
    text: 'JS 공부하기'
  },
  {
    text: 'JS 복습하기'
  }
]

```

`const todoList = new TodoList(data);`와 같은 형태로 파라메터를 넘기고, 생성해서 사용합니다.

+ 해당 컴포넌트에 render 함수를 작성합니다.
    
    + 이 함수는 파라메터로 넘겨받은 data를 순회하며 각 배열첨자의 text를 html string으로 만든 뒤,   
      todo-list라는 id를 가진 div에 innerHTML을 이용해 렌더링 되도록 합니다.

    + 이 함수는 별도의 파라메터 없이 todoList.render() 형태로 실행되도록 만듭니다.


## 소스코드 

```html 
<div id="todo-list"></div> 
``` 

```js 
    const data = [
        {
            text: 'JS 공부하기'
        },
        {
            text: 'JS 복습하기'
        }
    ];

    function TodoList(data) {
        this.render = function () {
            data.forEach((item) => {// 객체의 순회를 위해 값에 forEach문 사용 
                /* console을 통해서 data 는 객체의 형태로 출력된다.*/
                document.querySelector('#todo-list').innerHTML += `<div> 오늘의 할 일은 ${item.text} 입니다!!</div>`;
                /* 
                1. data 객체의 text 값에 접근하기 위해서 data.text를 사용 
                    
                2. innerHTML은 반복문을 통해 가장 마지막에 할당된 갚으로 덮어쓰기를 진행하기 때문에 =만 사용한다면 
                   1개의 div태그만 출력이 되는걸 확인할 수 있다. 이 문제를 해결하기 위해서는 +=를 사용해 
                   innerHTML을 이어쓰기 방식으로 div태그가 이어서 출력 되는걸 확인 가능하다  
                 */
                }
            );
        }
    }
        const todoList = new TodoList(data);
        todoList.render();
``` 

## render 함수 
+ data 객체에서 값의 순회를 위해 forEach 문을 사용하였다. 
    + data 객체 각각의 요소를 매개변수로 받아 진행한다. 위 코드에서는 2개의 변수를 받고 반복문을 2번 진행한다.      
    + item 변수는 객체 각각의 요소를 받기위한 변수로 원하는대로 지정해줘도 좋지만 일반적으로 item이라는 변수를 사용한다.    
<br>
+ document.querySelector를 통해 id 값이 todo-list인 html 요소에 접근할 수 있다. 
    + innerHTML을 사용해 id가 todo-list인 div 태그에 원하는 html 태그와 텍스트를 넣을 수 있다.    

```toc
``` 