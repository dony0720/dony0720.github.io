---
emoji: 🧢
title: TodoList (9)  - List 작성
date: '2023-03-28 16:30:00'
author: Js 
tags: TodoList 작성 
categories: TodoList Js 
---
# List 작성하기 구현 

## 소스코드 


```js
const toDoForm = document.querySelector(".todo");
const toDoList = document.getElementById("todo-list");
const toDoInput = document.querySelector(".todo input");
let toDos = [];
const TODOS_KEY = "todos";

function handleToDoSubmit(event){ 
  event.preventDefault();
  const newToDo = toDoInput.value ; 
  toDoInput.value = ""; 
  const newTodoObj = {
    text: newToDo,
    id: Date.now(),  
  };
  toDos.push(newTodoObj);
  paintToDo(newTodoObj);
  saveToDos();
 }
 
toDoForm.addEventListener("submit",handleToDoSubmit);

function paintToDo(newToDo){
const li = document.createElement("li"); 
li.id = newToDo.id; 
const span1 = document.createElement("span");
span1.innerText = newToDo.text;
const span2 = document.createElement("span")
span2.className = "material-symbols-outlined";
span2.innerText = "delete"
span2.addEventListener("click",deletToDo);
li.appendChild(span1);   
li.appendChild(span2);

toDoList.appendChild(li); 

}

function saveToDos(){
    localStorage.setItem(TODOS_KEY, JSON.stringify(toDos)); 
    // JSON.stringify는 string으로 바꾸는 역할을 한다. 
}

function deletToDo(event){
    const li = (event.target.parentElement); 
    // target은 클릭된 HTML의 element, parentElement는 클릭된 element의 부모 
    li.remove();
    toDos = toDos.filter((todo) => todo.id !== parseInt(li.id)); 
    //todo는 todos 각각의 object를 부르게 될 때 필요한 저장공간  
    saveToDos();
}

const savedToDos = localStorage.getItem(TODOS_KEY);

if (savedToDos !== null) { //저장된 데이터가 있을경우에 실행 
  const parsedToDos = JSON.parse(savedToDos); 
  //JSON.parse는 object로 바꾸는 역할을 한다 

  toDos = parsedToDos;
  parsedToDos.forEach(paintToDo); 
  // 각각의 item에 대해서 paintToDo를 실행시킨다 
  // parsedToDos가 4개의 인덱스를 가지고 있는 배열이라면 console.log를 각각의 인덱스에 대해서 총 4번실행하게 된다. 
}
```

## handleToDoSubmit(event) 함수


```js
function handleToDoSubmit(event){ 
  event.preventDefault();
  const newToDo = toDoInput.value ;
  toDoInput.value = "";
  const newTodoObj = {
    text: newToDo,
    id: Date.now(), 
  };
  toDos.push(newTodoObj);
  paintToDo(newTodoObj);
  saveToDos();
 }
```

1. `function handleToDoSubmit(event)` javascript가 발생한 event를    
      함수의 첫번째 인자로 주게된다. 

2. `event.preventDefault();` event의 기본 동작을 막는다 

3. newToDo에 input의 값을 저장하고 엔터를 누를때 input을 비우기 위해 `toDoInput.value = ""` 사용  

4. newTodoObj 객체를 생성하고 text 에는 **newToDo**를 각 리스트의    
   분별력을 주기 위해서 id 값을 `Date.now()` 리스트가 작성된 시간으로 반영

5. 할당된 객체는 **toDos** 배열에 채워넣는다 

## paintToDo()함수 


```js
function paintToDo(newToDoObj){
const li = document.createElement("li"); //li 태그 생성 
li.id = newToDoObj.id; 
const span1 = document.createElement("span");// span 태그 생성 
span1.innerText = newToDoObj.text;
const span2 = document.createElement("span")
span2.className = "material-symbols-outlined";
span2.innerText = "delete"
span2.addEventListener("click",deletToDo);
li.appendChild(span1); // span이 li의 자식으로 들어가진다  
li.appendChild(span2);

toDoList.appendChild(li); 
/*span -> li -> #todo-list 의 순서로 appendChild를 사용해야 
  역순으로 태그가 생성된다.*/
}
```

1. `const li = document.createElement("li")`    
    + li 태그 생성 


2. `li.id = newToDo.id` 
   + 생성된 li 태그의 id 값을 newTodoObj의 id로 할당 


3. `span1`도 `const li`와 동일한 원리로 할당 


4. **휴지통 아이콘을 클릭할때 마다 해당 list를 제거하기 위해서 `Google font`를 사용** 

    + `<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" />` 를 head에 작성 

    + `const span2 = document.createElement("span")1` 
       -> span 태그를 생성 

    + `span2.className = "material-symbols-outlined"` 
       -> 생성된 span2의 class명을 할당  

    + `span2.innerText = "delete"`
       -> 생성된 span2의 Text 값을 할당 


5. `li.appendChild(span1)`
    + `span1`이 `li`의 자식으로 들어가진다     
   
   `li.appendChild(span2)` 
    
    + `span1` 이 먼저 선언되었으므로 **li의 첫번째 후손으로 들어가고**    
    + `span2`가 **두번째 후손으로 들어가게된다** 


6. `toDoList.appendChild(li)` 
    + 생성된 li가 **`toDoList`** 의 자식으로 들어가게 된다. 

## saveToDos() 함수 


```js
function saveToDos(){
    localStorage.setItem(TODOS_KEY, JSON.stringify(toDos));
}
```

1. 생성된 리스트를 **`localStorage.setItem`** 을 이용해   
   key 값은 TODOS_KEY으로 Value는 **`JSON.stringify(toDos)`** 으로 저장한다 

2. **`JSON.stringify`** 는 toDos 배열을 **String**으로 바꾼다 

## deletToDo() 함수 


```js
function deletToDo(event){
    const li = (event.target.parentElement); 
    // target은 클릭된 HTML의 element, parentElement는 클릭된 element의 부모 

    li.remove();
    toDos = toDos.filter((todo) => todo.id !== parseInt(li.id)); 
    //todo는 todos 각각의 object를 부르게 될 때 필요한 저장공간  
    saveToDos();
}
```

1. `const li = (event.target.parentElement)` 
   -> target은 클릭된 HTML의 element, parentElement는 클릭된 element의 부모 

2. `li.remove();`
   -> 선택된 li태그를 제거한다 

3. ` toDos = toDos.filter((todo) => todo.id !== parseInt(li.id))` 

    + todo는 todos 각각의 object를 부르게 될 때 필요한 저장공간   

    + **`filter`함수의** 참 조건은 **toDos 배열안에 있는 각각의 id 값이**   
       **li.id** 값과 다를때이다   

    + 두 값을 비교하기 위해서 문자열인 li.id를 숫자로 변환시켜야 하므로     
       `parseInt` 를 사용한다 

## Local Strage에 저장된 값이 있을 경우 리스트 출력 구현 


```js
const savedToDos = localStorage.getItem(TODOS_KEY);

if (savedToDos !== null) { //저장된 데이터가 있을경우에 실행 
  const parsedToDos = JSON.parse(savedToDos); //JSON.parse는 object로 바꾸는 역할을 한다 
  toDos = parsedToDos;
  parsedToDos.forEach(paintToDo); 
  // 각각의 item에 대해서 paintToDo를 실행시킨다 
  // parsedToDos가 4개의 인덱스를 가지고 있는 배열이라면 painToDo를 각각의 인덱스에 대해서 총 4번실행하게 된다. 
}
```

1. savedToDos 변수를 만들고 `localStorage.getItem(TODOS_KEY)` 
   
   + key값이 TODOS_KEY로부터 저장된 데이터를 가져온다   

2. `if (savedToDos !== null)` 
    
    + 저장된 데이터가 있을경우에만 실행된다 

3. `const parsedToDos = JSON.parse(savedToDos);`    
  
    + `JSON.parse`**는 object로 바꾸는 역할을 한다

4. `parsedToDos.forEach(paintToDo);` 

    + **각각의 item에 대해서 paintToDo를 실행시킨다**   

    + **parsedToDos가 4개의 인덱스를 가지고 있는 배열이라면 paindToDo를 각각의 인덱스에 대해서 총 4번 실행하게 된다.**  
