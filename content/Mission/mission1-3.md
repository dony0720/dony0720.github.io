---
emoji: 📝
title: Js_mission - 다중 컴포넌트  
date: '2023-05-16 09:30:00'
author: 중석 
tags: Mission
categories: Mission  
---

# 필수 구현 사항 

## html 
+ `<div id="todo-list"></div>` 외의 다른 div를 두 개 더 html 코드에 만듭니다.  

+ `div`의 `id`는 적당한 이름으로 지어주세요.  

## js
+ `const data = [{ ... }]` 외에 todo를 담고 있는 array data를 두 개 더 만듭니다. 

+ todo의 내용은 본인의 현재 todo를 담아서 넣으면 더 좋겠죠?

+ `TodoList` 컴포넌트를 총 세 개 만듭니다. 첫 번째 컴포넌트에는 제가 넣어둔 data와 #todo-list에 렌더링하고,    
  나머지 두 개는 여러분이 추가하신 div + data를 활용해서 만들어주세요.




## 소스코드 

### html 
```html 
   <div id="todo-list"></div>
    <div id="todo-worship"></div>
    <div id="todo-workout"></div>
``` 

### js 
```js 
     const todo_study = [
            {
                text: 'HTML'
            },
            {
                text: 'Css'
            },
            {
                text: 'Javascript'
            }

        ];

        const todo_worship = [
            {
                text: '콘티 정하기'
            },

            {
                text: '콘티 key 수정하기'
            }
        ]

        const todo_workout = [
            {
                text: '웨이트 운동하기'
            },

            {
                text: '유산소 운동하기'
            }

        ]

        function TodoList(data, id) {

            /* 인스턴스 확인 */
            if (!new.target) {
                throw new Error("is not instance");
            }

            if (!data) {
                throw new Error("check Null or Undefined");
            }

            this.render = function () {
                data.forEach((item) => {
                    document.querySelector(`${id}`).innerHTML += `<div> 오늘의 할 일은 ${item.text} 입니다!!</div>`;
                }
                )
            }
        }
      
        const study = new TodoList(todo_study,"#todo-list");
        const worship = new TodoList(todo_worship,"#todo-worship");
        const workout = new TodoList(todo_workout,"#todo-workout");

        study.render();
        worship.render();
        workout.render();
``` 

## TodoList에 id 매개변수 추가 
+ 함수에 id 매개변수를 추가해서 document.querySelector를 통해 해당 id 값을 가진 div태그에 접근한다. 
+ 각 컴포넌트에 해당되는 data가 출력이 되는걸 볼 수 있다

## 결과 
![결과3](mission_result\result_3.png) 
```toc
``` 