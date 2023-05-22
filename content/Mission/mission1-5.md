---
emoji: 📝
title: Js_mission - setState() 함수    
date: '2023-05-16 09:30:00'
author: Js 
tags: Mission
categories: Mission  
---

# 필수 구현 사항 

## js
TodoList 함수에 setState(nextData)라는 함수를 만듭니다
+ 이 함수는 해당 컴포넌트 초기 생성 시 넘겼던 data 파라메터를 nextData로 대체하고 
+ 컴포넌트를 다시 렌더링합니다.
  
해당 함수를 추가한 뒤, new TodoList(...) 하는 코드 이후에 해당 컴포넌트의 인스턴스에    
todoList.setState(새로운 배열) 형태로 데이터만 다시 넣었을 때 컴포넌트가 다시 렌더링 되도록 작성해주세요.

+ setState 함수 호출 후 다시 todoList.render()를 호출하는 것이 아니라,    
  setState 함수 내에서 화면을 다시 렌더링하는 것까지 처리해야 합니다.
 
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

        const nextdata = [
            {
                text: '닭가슴살 먹기',
                isCompleted: false
            },

            {
                text: '맛있게 치킨 먹기',
                isCompleted: false
            }
        ]

        function checkData(data) {
            /* Null or Undefined일 경우 false가 반영해 if문 실행 */
            if (!data) {
                throw new Error("check Null or Undefined");
            }

            if (!Array.isArray(data)) {
                throw new Error("todoList is not Array");
            }
        }

        function TodoList(data, id) {
            /* setState는 인스턴스가 생성되어야 동작하므로 초기에 체크하면됨*/
            if (!new.target) {
                throw new Error("is not instance");
            }

            checkData(data);

            this.render = function () {
                data.forEach((item) => {
                    if (item.isCompleted === true) {
                        const todo = `<div><s>오늘의 할 일은 ${item.text} 입니다!!<s></div>`;
                        document.querySelector(`${id}`).insertAdjacentHTML("beforeend", todo)
                    }
                    else {
                        const todo = `<div>오늘의 할 일은 ${item.text} 입니다!!</div>`;
                        document.querySelector(`${id}`).insertAdjacentHTML("beforeend", todo)
                    }
                })
            }

            this.setState = function (nextdata) {
                data = nextdata;
                checkData(data);
                document.querySelector(`${id}`).innerHTML = ``;
                this.render();
            }
        }



        const study = new TodoList(todo_study, "#todo-list")

        study.render();
        study.setState(nextdata);
``` 

## render 함수
+ insertAdjacentHTML을 적용해 += 복합연산자를 사용하지 않는다. 
    
## setState 함수   
+ TodoList 함수는 data를 매개변수로 받고 있기 때문에 data = nextdata로 설정해    
  render 함수가 문제 없이 동작하게 한다 
+ 외부에 선언된 checkData() 함수를 호출해 nextData의 유효성을 검증한다. 
+ 유효성 검증이 마치고 `innerHtml = ''` 통해 기존 데이터를 초기화 시킨후에    
  render 함수를 호출해 nextdata의 내용을 렌더링한다. 

## 결과 
![결과5-1](mission_result\result_5.1.png) 
![결과5-2](mission_result\result_5.2.png) 
```toc
``` 