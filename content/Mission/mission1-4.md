---
emoji: 📝
title: Js_mission - isCompleted 추가   
date: '2023-05-16 09:30:00'
author: 중석 
tags: Mission
categories: Mission  
---

# 필수 구현 사항 

## js
+ data의 각 object에 `text`외에 `isCompleted` 라는 필드를 추가합니다. 

+ 해당 값은 true, 혹은 false 값을 지정해주세요.

```js
const data = [
  { 
    text: '코딩하기',
    isCompleted: true
  },
  {
    text: '집안 청소하기',
    isCompleted: false
  }
]
``` 
+ `TodoList` 컴포넌트 내에 text 렌더링 시, isCompleted 값이 true인 경우 `<s>` 태그를 이용해    
  삭선처리를 해주는 걸 추가합니다.


## 소스코드 


### js 
```js 
     const todo_study = [
            {
                text: 'HTML',
                isCompleted: true
            },
            {
                text: 'Css',
                isCompleted: false
            },
            {
                text: 'Javascript',
                isCompleted: true
            }

        ];

        const todo_worship = [
            {
                text: '콘티 정하기',
                isCompleted: true
            },

            {
                text: '콘티 key 수정하기',
                isCompleted: false
            }
        ]

        const todo_workout = [
            {
                text: '웨이트 운동하기',
                isCompleted: false
            },

            {
                text: '유산소 운동하기',
                isCompleted: true
            }

        ]

        function TodoList(data, id) {
            /* 인스턴스 확인 */
            if (!new.target) {
                throw new Error("is not instance");


            this.render = function () {
                data.forEach((item) => {
                    if (item.isCompleted === true) {
                        document.querySelector(`${id}`).innerHTML += `<div><s>오늘의 할 일은 ${item.text} 입니다!!<s></div>`;
                    }
                    else {
                        document.querySelector(`${id}`).innerHTML += `<div>오늘의 할 일은 ${item.text} 입니다!!</div>`;
                    }
                }
                )
            } 
            }
        }
        const study = new TodoList(todo_study, "#todo-list");
        const worship = new TodoList(todo_worship, "#todo-worship");
        const workout = new TodoList(todo_workout, "#todo-workout");

        study.render();
        worship.render();
        workout.render();
``` 

## render 함수의 isCompleted 값에 따른 삭선 추가 
+ item.isCompleted 를 통해 true or false 값에 접근한다.  
+ if 문을 사용해 isCompleted 값이 true면 `<s>` 태그가 추가된다. 
+ 반대로 isCompleted 값이 false면 `<s>` 태그 없이 생성된다.

## 결과 
![결과4](mission_result\result_4.png) 
```toc
``` 