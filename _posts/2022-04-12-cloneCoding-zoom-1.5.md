---
title: "[SocketIO] Nomad Coders 줌 클론코딩 #1.5"
published: true
categories:
  - zoomClone
---

## Connect WebSocket

<br>

<script src="https://gist.github.com/seulgi9506/d84308093e255a7fbd575f7e6a53b220.js"></script>

<br><br>

### HTTP vs WebSocket

> ##### http
>
> - request / response 구조.
> - request를 해야지만 response를 받을 수 있음.
> - 서버가 먼저 response를 보낼 순 없음.
> - 서버는 유저를 기억할 수 없음.
> - request로 쿠키를 보내야 유저가 누구인 지 알 수 있음.
> - stateless
>   <br>
>
> ##### WebSocket
>
> - 유저가 request를 하면 서버가 accept 또는 deny 할 수 있음.
> - 한 번 accept되면(connection 된 상태) 서버가 유저에게 메세지를 보낼 수도 있고 유저도 서버에게 메세지를 보낼 수 있음.
> - 서버는 request를 기다리지 않음.
> - 한 번 연결되면 서버는 유저를 기억함.
> - 서로에게 직접 접근이 가능
> - 브라우저와 backend 사이 / backend와 backend 사이에서 발생 할 수 있음.
> - bi-directional(양뱡향) 연결

<br><br><br><br>

### WebSocket 설치

<br>

    npm i ws

명령어로 설치한다.<br>express는 http를 다루기 때문에 ws과는 다른 protocol이다. <br>같은 서버에 ws 기능을 합쳐야하는데, Node.js에 내장되어있는 http package를 사용해서 합칠 수 있다.

<br><br><br><br>

### WebSocket 서버와 http 서버 합치기

<br>

##### **<mark style="background-color: #d4d4f8">import http from "http";</mark>**<br><br>

##### **<mark style="background-color: #d4d4f8">import WebSocket from "ws";</mark>**<br><br>

##### **<mark style="background-color: #d4d4f8">const server = http.createServer(app);</mark>**

http서버에 access<br><br>

##### **<mark style="background-color: #d4d4f8">const wss = new WebSocket.Server({ server });</mark>**

http서버 위에 WebSocket 서버 만들기<br><br>

localhost가 동일한 포트에서 http, ws request 두 개를 다 처리할 수 있다.

<br><br><br><br>

### FrontEnd와 BackEnd 연결하기

<br>

frontend에서 backend로 연결하는 방법은 아래 코드를 사용하는 것임.<br>
![image](https://user-images.githubusercontent.com/102353910/162972154-8d8ff9bf-ea10-4fbf-8ff9-b069bc390afd.png)

[👉참고](https://developer.mozilla.org/ko/docs/Web/API/WebSocket/WebSocket)

<br>

    const socket = new WebSocket("ws://localhost:3003");

이렇게 하면 작동하기는 함.<br>하지만 나중에 핸드폰에서 보면 작동안함.<br>당연히 폰은 localhost:3003이 존재하지 않기 때문.<br>브라우저가 스스로 주소를 가져오도록 해야 함.
<br><br>

![image](https://user-images.githubusercontent.com/102353910/162972638-a62ff6da-b5cc-4279-9c58-1519c92530e3.png)

##### **<mark style="background-color: #d4d4f8">window.location</mark> 사용**<br>

    const  socket  =  new  WebSocket(`ws://${window.location.host}`);

<br>

이렇게 연결해주고 server.js에서 아래 코드를 입력해서 실행시키면 콘솔에서 WebSocket을 확인할 수 있다.
<br>

    wss.on("connection", (socket) => {
      console.log(socket);
    });

<br>

![image](https://user-images.githubusercontent.com/102353910/162973619-8bca95b0-b88e-4d86-9f5c-31347bba6639.png)
<br>

> #### **.on("event", function)**
>
> js의 function과 eventListener처럼 WebSocket도 listen할 수 있는 특정한 event명이 있다.
> close, connection, error, header, listening 이벤트가 있다.
> connection은 누군가 우리와 연결됐다는 것이다. 이 method의 설명을 보면 callback으로 socket을 받는다고 한다.

<br><br>

    wss.on("connection", (socket) => {
      socket.send("hello!");
    });

<br>

server.js에서 익명함수로 메세지 보냄.
<br><br>
![image](https://user-images.githubusercontent.com/102353910/162974767-11b8a678-9a89-42ef-99c2-a9729c01c9e4.png)

<br>
app.js에서 받음.

<br><br><br><br>

### 🚫오류🚫

<br>

![image](https://user-images.githubusercontent.com/102353910/162975202-de0b700e-0e27-47e8-8ebe-85f3f390cd52.png)

<br>

콘솔에 "hello from the browser!"가 출력되어야 하는데 이상한 숫자들이 나옴.

<br>

### 🆗해결🆗

<br>

![image](https://user-images.githubusercontent.com/102353910/162975439-1bc5bd99-9f37-40a7-a8cd-04cf6d12c8fc.png)

<br>

<mark style="background-color: #f2ea6e">toString("utf-8")</mark> 으로 해결

<br><br><br><br>
