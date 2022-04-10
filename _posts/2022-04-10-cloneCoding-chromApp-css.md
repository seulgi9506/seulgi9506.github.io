---
title: "[Vanilla JS] Nomad Coders 바닐라 JS로 크롬 앱 만들기 #CSS"
published: true
categories:
  - Momentum
---

## CSS

<br>

### style.css

```css
@import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");

body {
  font-family: "Inter", sans-serif;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  margin: 0px;
  position: relative;
}

body,
html {
  overflow: hidden;
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 0;
}

img {
  font-weight: bold;
  object-fit: cover;
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: -1;
}

input {
  background: none;
  appearance: none;
  border: 0;
  color: white;
  border-bottom: 2px solid white;
}

input::placeholder {
  color: white;
}

input:focus {
  outline: none;
}

.hidden {
  display: none;
}

#info-div {
  display: grid;
  grid-template-columns: auto;
  row-gap: 10px;
  grid-template-areas:
    "clock"
    "name"
    "todo";
  place-items: center center;
  align-content: center;
  justify-content: center;
  flex-direction: column;
}

#clock-div {
  grid-area: clock;
  align-self: start;
  display: block;
  margin-top: 0px;
  margin-bottom: 0px;
}

#clock {
  font-size: 12em;
  font-weight: bold;
  margin: 0;
  text-shadow: 4px 4px 5px #353535;
}

#login-div {
  grid-area: name;
  align-self: center;
  display: block;
}

#login-form {
  border: none;
  color: white;
  font-size: 36px;
  margin-bottom: 20px;
}

#login-form input {
  font-size: 32px;
  text-shadow: 1px 1px 3px #353535;
}

#greeting {
  font-size: 40px;
  margin-bottom: 20px;
  text-shadow: 2px 2px 3px #353535;
}

#todo-div {
  grid-area: todo;
  align-self: end;
  display: block;
}

#todo-form input {
  padding-top: 20px;
  font-size: 26px;
  text-shadow: 1px 1px 3px #353535;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  margin-top: 20px;
  display: block;
}

li {
  font-size: 22px;
  text-shadow: 1px 1px 3px #353535;
  padding: 3px;
}

#todo_button {
  margin-right: 10px;
  cursor: pointer;
  background: none;
  appearance: none;
  border: 0;
}

#quote {
  position: absolute;
  bottom: 20px;
}

#weather {
  position: absolute;
  top: 2%;
  right: 2%;
  text-align: right;
}

#weather_span {
  display: block;
}

#city_span {
  display: block;
}
```

<br>

CSS의 향연~~<br>

> #### 👉참고
>
> [1분코딩 '이번에야말로 CSS Grid를 익혀보자'](https://studiomeal.com/archives/533)

<br><br><br><br>

##### 여기까지 수행한 결과물

<br>

![image](https://user-images.githubusercontent.com/102353910/162608611-351df0d4-bcc8-448f-aa1f-1190a27c8871.png)

<br><br><br><br>
