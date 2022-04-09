---
title: "[Vanilla JS] Nomad Coders 바닐라 JS로 크롬 앱 만들기 #7"
published: true
categories:
  - Momentum
---

## To Do List

<br>

### todo.js<br>

```js
const toDoForm = document.getElementById("todo-form");
const toDoList = document.getElementById("todo-list");
const toDoInput = toDoForm.querySelector("input");

const TODOS_KEY = "todos";

let toDos = [];

function saveToDos() {
  localStorage.setItem(TODOS_KEY, JSON.stringify(toDos));
}

function deleteToDo(event) {
  const li = event.target.parentElement;
  li.remove();
  toDos = toDos.filter((toDo) => toDo.id !== parseInt(li.id));
  saveToDos();
}

function paintToDo(newTodo) {
  const li = document.createElement("li");
  li.id = newTodo.id;
  const span = document.createElement("span");
  span.innerText = newTodo.text;
  const button = document.createElement("button");
  button.innerText = "❌";
  button.addEventListener("click", deleteToDo);
  li.appendChild(span);
  li.appendChild(button);
  toDoList.appendChild(li);
}

function handleToDoSubmit(event) {
  event.preventDefault();
  const newTodo = toDoInput.value;
  toDoInput.value = "";
  const newTodoObj = {
    text: newTodo,
    id: Date.now(),
  };
  toDos.push(newTodoObj);
  paintToDo(newTodoObj);
  saveToDos();
}

toDoForm.addEventListener("submit", handleToDoSubmit);

const savedToDos = localStorage.getItem(TODOS_KEY);

if (savedToDos) {
  const parsedToDos = JSON.parse(savedToDos);
  toDos = parsedToDos;
  parsedToDos.forEach(paintToDo);
}
```

<br>

### index.html 추가

<br>

```html
<form id="todo-form">
  <input type="text" placeholder="Write a To Do and Press Enter" required />
</form>
<ul id="todo-list"></ul>
```

<br><br>

#### 위에서부터 설명💫

<br><br>

**<mark style="background-color: #64c6e3">let toDos</mark><br>input에 입력한 todo list를 저장하기 위한 빈 배열 선언**<br><br>

**<mark style="background-color: #d4d4f8">function saveToDos()</mark> <br> 사용자가 input에 입력한 값을 받아서 <br>TODOS_KEY에 저장된 todos 라는 키값으로 localStorage에 저장**<br><br>

**<mark style="background-color: #d4d4f8">function deleteToDo()</mark><br>todo list를 삭제하기 위한 함수**<br>어떤 li태그를 삭제할 것인지 target.parentElement로 알려줌. <br>localStorage에도 똑같이 삭제해줘야한다. <br>localStorage에 저장된 요소의 키값인 id값을 이용해 삭제해준다.<br>이때 배열에서 해당 값을 삭제하는 개념이 아닌,<br>삭제할 값을 제외한 나머지들을 다시 저장해 주는 개념이다.<br> <mark style="background-color: #f2ea6e">.filter()</mark>를 이용하면 true 값을 제외한 값을 리턴시킨다. <br> 그리고 다시 saveToDos()를 실행해 localStorage에 저장된 값을 바꿔준다.<br><br>

**<mark style="background-color: #d4d4f8">function paintToDo()</mark><br>input태그에 입력한 값을 화면에 보여주는 함수** <br>사용자가 input에 새로운 데이터를 입력하면 <br>ul태그 안에 li태그와 span태그, button태그가 만들어진다.<br>태그를 만들 때 로컬에 키가 id로 저장된 값이 li태그의 id값으로 생성된다.<br>span태그도 마찬가지로 로컬의 키가 text인 value값을 가져와 innerText로 적용된다.<br>버튼을 누르면 값이 삭제되어야 하므로 <br> <mark style="background-color: #f2ea6e">addEventListener()</mark>를 이용해 버튼이 클릭되면 deleteToDo()를 실행해 삭제할수 있도록 해준다.<br><br>

**<mark style="background-color: #d4d4f8">function handleToDoSubmit()</mark>** <br>**input에 값을 입력하고 엔터를 누르면 실행되는 함수**<br>submit하면 페이지가 새로고침되는 것을 막기 위해 <mark style="background-color: #f2ea6e">preventDefault()</mark> 사용<br>input의 value값을 newTodo에 저장하고 input칸을 비워주기<br>newTodoObj는 input에 입력한 value값을 text로 저장, **각 값을 구분하기 위해** id값을 Date.now()로 줘서 구분<br>Date.now()는 시간을 ms단위로 가져오기 때문에 랜덤한 수처럼 보임<br>=>id값으로 사용하기 적절함<br>맨 위에서 만들어준 빈 배열에 newTodoObj를 저장한 뒤<br>화면에 출력해주는 paintToDo()와 localStorage에 저장해주는 saveToDos()를 실행<br><br>

**<mark style="background-color: #a7e8c8">맨 아래 if문</mark>**<br>만약 localStorage에 todos 값이 있으면 <mark style="background-color: #f2ea6e">JSON.parse</mark>를 이용해 배열로 바꿔서 toDos에 저장하고 배열로 바꿔진 값을 들고가서 paintToDo 함수를 실행.<br>JSON.parse를 사용하는 이유는 localStorage에는 String형태로만 저장이 되기 때문이다.<br>배열처럼 보여도 콘솔에 출력해보면 문자열로 출력된다.

<br><br><br><br>

##### 여기까지 수행한 결과물

<br>

![image](https://user-images.githubusercontent.com/102353910/162563064-f76e3834-81ad-43d2-811f-f113894a93c1.png)

<br><br><br><br>
