---
title: "[Vanilla JS] Nomad Coders 바닐라 JS로 크롬 앱 만들기 #4 #5"
published: true
categories:
  - Momentum
---

## Login & Clock

<br>

### index.html

<br>

```xml
<!DOCTYPE  html>
<html  lang="en">
  <head>
    <meta  charset="UTF-8" />
    <meta  http-equiv="X-UA-Compatible"  content="IE=edge" />
    <meta  name="viewport"  content="width=device-width, initial-scale=1.0" />
    <link  rel="stylesheet"  href="css/style.css" />
    <title>Momentum</title>
  </head>
  <body>
    <form  id="login-form"  class="hidden">
      <input
        required
        maxlength="15"
        type="text"
        placeholder="What is your name?"
      />
      <input  type="submit"  value="Log In" />
    </form>
    <h2  id="clock">00:00:00</h2>
    <h1  id="greeting"  class="hidden"></h1>
    <script  src="js/greeting.js"></script>
    <script  src="js/clock.js"></script>
  </body>
</html>
```

<br>

- input태그 : 사용자 이름을 입력 받기 위함
- h2태그 : 시계 표시하기 위한 태그
- h1태그 : 사용자 이름을 입력 받고 나서 hello 메세지를 띄우기 위한 태그
- 한 번 local storage에 이름이 저장되면 더 이상 input태그를 띄우지 않고 hello 메세지만 띄운다.<br>=>두 태그 모두 css에서 display: none 으로 숨겼다가 상황에 맞는 것을 노출시킨다.
- 다음과 같은 코드가 필요하다고 생각했지만 필요치 않다.<br>

```js
function handleLoginBtn() {
  const username = document.querySelector("#login-form input").value;
  if (username === "") {
    alert("Please write your name.");
  } else if (username.length > 15) {
    alert("Your name is too long");
  }
}
```

- input태그의 **<mark style="background-color: #d4d4f8">required</mark>** 속성을 이용하여 필수로 필요한 값임을 알릴 수 있다.
- input태그의 **<mark style="background-color: #d4d4f8">maxlength</mark>** 속성을 이용하여 최대로 입력할 수 있는 길이를 설정할 수 있다.

<br><br>

### greeting.js

<br>

```javascript
const loginForm = document.querySelector("#login-form");
const loginInput = document.querySelector("#login-form input");
const greeting = document.querySelector("#greeting");

const HIDDEN_CLASSNAME = "hidden";
const USERNAME_KEY = "username";

function onLoginSubmit(event) {
  event.preventDefault();
  loginForm.classList.add(HIDDEN_CLASSNAME);
  const username = loginInput.value;
  localStorage.setItem(USERNAME_KEY, username);
  paintGreetings(username);
}

function paintGreetings(username) {
  greeting.innerText = `Hello ${username}`;
  greeting.classList.remove(HIDDEN_CLASSNAME);
}

const savedUsername = localStorage.getItem(USERNAME_KEY);

if (savedUsername === null) {
  loginForm.classList.remove(HIDDEN_CLASSNAME);
  loginForm.addEventListener("submit", onLoginSubmit);
} else {
  paintGreetings(savedUsername);
}
```

<br>

- 지난 시간에 학습했던 <mark style="background-color: #d4d4f8">classList</mark> 를 이용하여 태그에 클래스 이름을 추가하거나 제거할 수 있다.
- **<mark style="background-color: #d4d4f8">classList.add</mark>**
- **<mark style="background-color: #d4d4f8">classList.remove</mark>**
- **<mark style="background-color: #d4d4f8">preventDefault()</mark>** 를 이용하여 각 명령들의 기본 동작을 막을 수 있다.<br>=> 여기에서는 form에서 submit하면 페이지가 새로고침 되는 것을 막고 있다.
- onLoginSubmit() 함수에서 input태그의 value값으로 <mark style="background-color: #f4a2a4">'username'</mark> 을 가져오고 있다.
- 가져온 <mark style="background-color: #f4a2a4">'username'</mark>은 **<mark style="background-color: #d4d4f8">localStorage.setItem()</mark>** 을 이용해서 <mark style="background-color: #64c6e3">"username"</mark>이라는 키값으로 input.value인 <mark style="background-color: #f4a2a4">'username'</mark>을 저장하고있다.
- paintGreetings() 함수에서는 h1 태그의 텍스트를 바꾸고 display: none 이 적용된 hidden이라는 클래스네임을 제거해준다.
- 아래에서 부터는 사용자가 입력한 <mark style="background-color: #f4a2a4">'username'</mark>이 아닌 localStorage에 저장된 username을 **<mark style="background-color: #d4d4f8">localStorage.getItem()</mark>** 으로 가져와서 비교한다.
- 만약 localStorage에 키값이 username으로 등록된 value가 없다면 form태그에서 display: none 이 적용된 클래스네임 hidden 을 없애고 input태그를 보여준다.
- 반대로 username으로 등록된 value가 있다면 paintGreetings()를 실행한다.

<br><br>

### clock.js

<br>

```javascript
const clock = document.querySelector("h2#clock");

function getClock() {
  const date = new Date();
  const hours = String(date.getHours()).padStart(2, "0");
  const minutes = String(date.getMinutes()).padStart(2, "0");
  const seconds = String(date.getSeconds()).padStart(2, "0");
  clock.innerText = `${hours}:${minutes}:${seconds}`;
}

getClock();
setInterval(getClock, 1000);
```

<br><br>
아래처럼 <mark style="background-color: #d4d4f8">new Date()</mark> 로 현재 날짜와 시간에 대한 정보를 알 수 있다.<br>뿐만 아니라 날짜, 요일, 년도, 시간, 분, 초 등 필요한 데이터만 꺼내올 수 도 있다.
<br><br>

![image](https://user-images.githubusercontent.com/102353910/162447002-59eea182-0f99-4c12-a561-4304a1848736.png)
<br><br>

하지만 01초, 02초, 03분, 04시 처럼 한 자리 숫자는 0을 포함하지 않고 한 자리만 가져온다.<br>만약 그렇게 표시된다면 (만든 입장에서) 보기에 매우 불편하다.<br>그러면 한 자리 수인지 아닌지 검사해서 맞으면 앞에 0을 붙여주고, 아니라면 그냥 표시해주는 로직을 짠다면 어떨까? 라고 생각했다.<br>하지만 내가 틀렸다.<br>이미 천재들이 <mark style="background-color: #d4d4f8">padStart</mark> 라는 아주 lazy하고 갓벽한 것을 만들어 놨기 때문이다.

<br><br>

![image](https://user-images.githubusercontent.com/102353910/162448401-45537b0a-2814-496b-b362-4145abca69e9.png)

<br><br>

> "문자열".padStart(원하는 길이, "충족하지 못할 시에 앞쪽으로 대신 넣을 값")

<br>이렇게 사용한다.<br>궁금해서 세 자릿수, 열 자릿수도 써봤다.<br> 아주 대단하다....!<br>뿐만 아니라 입력한 값 뒤로 취가하는 padEnd도 있다.<br><br>이제 필요한 값을 다 가져왔지만 아직까지는 웹페이지가 실행 된 현재 시간만을 가져올 뿐 시계는 움직이지 않는다.<br>시계를 움직이게 하기 위해 <mark style="background-color: #d4d4f8">interval()</mark> 을 사용했다.<br>괄호 안에 동작하길 원하는 함수 명을 넣으면 일정 시간을 두고 계속해서 명시한 함수를 실행해준다.<br>함수명 뒤에 시간을 설정할 수 있다. 단위는 ms(millisecond)이다.<br>ms에 1000을 넣어주면 이제 1초마다 현재 시간이 업데이트되면서 시계가 움직인다. <br>하지만 페이지를 실행하고 1초뒤에 시계가 나타나게 되어버리니까 처음 한 번은 시계를 직접 호출해서 실행해줬다.

<br><br>

### style.css

```css
.hidden {
  display: none;
}
```

<br><br><br><br>
