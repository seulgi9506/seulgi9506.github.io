---
title: "[SocketIO] Nomad Coders 줌 클론코딩 #2"
published: true
categories:
  - zoomClone
---

## Socket.io

<br>

지난 시간에는 WebSocket을 이용해 브라우저끼리 연결하고 메세지를 주고 받는 기능을 만들었다.<br>그리고 오늘은 Socket.io를 이용해 더 쉽게 만드는 방법을 배웠다.<br>
<br>

### Socket.io란?

- [ ] 쉽게 프론트엔드와 백엔드 간의 실시간 통신을 가능하게 해주는 framework이다.
- [ ] 실시간 기능을 더 쉽게 만드는 편리한 코드를 제공한다.
- [ ] WebSocket의 부가기능이 아니다.
- [ ] WebSocket을 지원하지 않으면 http long-polling을 사용한다.
- [ ] 와이파이가 끊기면 자동적으로 재연결을 시도한다.
- [ ] firewell이나 proxy가 있어도 사용가능하다.
- [ ] 모든 플랫폼, 모든 브라우저, 모든 디바이스에 이용 가능하다.

<br><br><br>

### Socket.io설치

    $ npm i socket.io

<br>

##### server.js

```js
import SocketIO from "socket.io";

const io = SocketIO(server);
```

<br>

##### home.pug

```html
script(src="/socket.io/socket/io.js")
```

<br><br><br>

![image](https://user-images.githubusercontent.com/102353910/163405464-91c33be4-5cb5-459e-acb7-746b7a85a09c.png)

<br>

Socket.io를 설치해주면 화면에서 io라는 fucntion을 볼 수 있다. <br>자동적으로 back-end socket.io와 연결해주는 function이다. <br>`app.js`에서 `const socket = io();` 만 써주면 이 io function은 알아서 socket.io를 실행하고있는 서버를 찾는다.

<br><br><br><br>

### Rooms

채팅을 할 수 있는 방을 만든다.<br>html에서 유저가 방을 만들거나 방에 참가할 수 있는 form을 만든다.<br>그 전까지는 오브젝트를 스트링으로 변환시키고 스트링을 전송했지만 socket.io는 그럴 필요가 없다.<br>객체를 바로 보낼 수 있다.<br>socket.io가 알아서 스트링으로 바꿔서 전달해주고 다시 알아서 자바스크립트 오브젝트로 만들어준다.

<br>

##### app.js

```js
function handelRoomSubmit(event) {
  event.preventDefault();
  const input = form.querySelector("input");
  socket.emit("enter_room", input.value, showRoom);
  roomName = input.value;
  input.value = "";
}

form.addEventListener("submit", handelRoomSubmit);
```

<br>

##### server.js

```js
io.on("connection", (socket) => {
  socket.on("enter_room", (roomName, showRoom) => {
    socket.join(roomName);
    showRoom();
    socket.to(roomName).emit("welcome", socket.nickname, countRoom(roomName));
    io.sockets.emit("room_change", publicRoom());
  });
});
```

<br>

> 이 때 argument는 자신이 원하는 만큼 보낼 수 있다. 객체 뿐만 아니라 함수도 보낼 수 있다.

<br><br><br><br>

### Adapter

![image](https://user-images.githubusercontent.com/102353910/163408926-d35058d0-c721-4d1d-a42a-e4c42e7f8bee.png)
[👉출처 : socket.io/docs/v4/adapter](https://socket.io/docs/v4/adapter/)

<br>
다른 서버들 사이에서 실시간 어플리케이션을 동기화하는 역할이다.<br>모든 클라이언트가 같은 서버에 연결되는 것은 아니다.<br>만약 서버 a에 있는 클라이언트가 서버b에 있는 클라이언트에게 메세지를 보내고 싶다면<br>메세지는 서버a에서 adapter와 데이터베이스를 거치고 다시 adapter로 가서 서버b의 클라이언트에게 전달된다.<br>adapter는 누가 연결되어있는지, 현재 어플리케이션에 room이 얼마나 있는지를 알려준다.

<br>

```js
console.log(io.sockets.adapter);
```

![image](https://user-images.githubusercontent.com/102353910/163409150-2208d999-7d65-4f27-bc40-2609484e9624.png)

<br>

adapter를 이용하면 방이 몇 개 있는지, 소켓이 몇 개 있는지 콘솔에서 확인할 수 있다.<br> 소켓의 id를 뜻하는 `sids`를 가져와서 rooms를 보고 이 방들이 어떤 socket을 위해 만들어졌는지 확인할 수 있다.<br> 만약 room id를 socket id 에서 찾을 수 있다면 private room<br>그렇지 않으면 public room 이다.

<br><br><br><br>

### ⚡코드

<script src="https://gist.github.com/seulgi9506/c7b80d72ecd004b5cad438ba1ec57990.js"></script>

<br><br><br><br>
