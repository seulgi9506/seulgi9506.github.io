---
title: "[SocketIO] Nomad Coders 줌 클론코딩 #1.9"
published: true
categories:
  - zoomClone
---

## Send Message

<br>

<script src="https://gist.github.com/seulgi9506/3fcafb2edd82f0ce863370e406238c16.js"></script>

<br><br>

### 다른 브라우저와 연결

<br>

현재까지 한 것은 서버와 브라우저 사이에서 혼자 대화하는 것이다.<br>다른 브라우저와 연결되어 있지 않으므로 의미가 없는 것이다.

<br>

```js
const sockets = [];
wss.on("connection", (socket) => {
  sockets.push(socket);
  socket.on("message", (message) => {
    console.log(message.toString("utf-8"));
  });
});
```

<br>
새로운 브라우저가 연결될 때 마다 sockets 배열에 넣어줬다.

<br>

![image](https://user-images.githubusercontent.com/102353910/163002162-04bf4e95-8d91-41db-af5c-eb0a0972f3ea.png)

<br>

서로 다른 브라우저에서 각각 입력해도 모두 콘솔에 표시되고 있다.<br>하지만 여전히 누가 보낸지는 알 수 없다.<br>그래서 누가 보냈는지 알 수 있도록 저장할 수 있는 form을 만들었다.

<br>

##### home.pug

```pug
doctype html
html(lang="en")
  head
    meta(charset="UTF-8")
    meta(http-equiv="X-UA-Compatible", content="IE=edge")
    meta(name="viewport", content="width=device-width, initial-scale=1.0")
    title Zoom
    link(rel="stylesheet", href="https://unpkg.com/mvp.css")
  body
    header
      h1 Zoom
    main
      form#nick
        input(type="text", placeholder="choose a nickname", required)
        button Save
      ul
      form#message
        input(type="text", placeholder="write a msg", required)
        button Send
    script(src="/public/js/app.js")
```

<br>

하지만 text가 두개라서 (닉네임과 메세지) 둘 다 메세지로 전송되어버린다.<br>JSON을 보내서 구분할 수 있도록 만들어줬다.

<br>

```js
function handleNickSubmit(event) {
  event.preventDefault();
  const input = nickForm.querySelector("input");
  socket.send({
    type: "nickname",
    payload: input.value,
  });
}
```

<br>

![image](https://user-images.githubusercontent.com/102353910/163004220-5a842c18-9ae1-4ea9-ab2c-c948be838d26.png)

<br>

하지만 닉네임을 입력하니 `[object Object]`로 출력되고 있다.<br>object를 가져와서 string으로 바꿔줘야한다.<br>**JSON.stringify** 를 사용했다.

<br>

##### app.js

```js
function makeMessage(type, payload) {
  const msg = { type, payload };
  return JSON.stringify(msg);
}

function handleSubmit(event) {
  event.preventDefault();
  const input = messageForm.querySelector("input");
  socket.send(makeMessage("new_message", input.value));
  input.value = "";
}

function handleNickSubmit(event) {
  event.preventDefault();
  const input = nickForm.querySelector("input");
  socket.send(makeMessage("nickname", input.value));
  input.value = "";
}
```

<br>

![image](https://user-images.githubusercontent.com/102353910/163005101-36a47e2e-1457-4ae7-9e37-301d073ac9b6.png)

<br>

그러고 나면 또 이런 혼돈의 카오스를 볼 수 있다.<br>다시 백엔드에서 **JSON.parse**를 이용해서 string을 자바스크립트 object로 바꿔줘야 한다.

<br>

##### server.js

```js
wss.on("connection", (socket) => {
  sockets.push(socket);
  socket["nickname"] = "Anonymouos";
  socket.on("message", (msg) => {
    const message = JSON.parse(msg);
    switch (message.type) {
      case "new_message":
        sockets.forEach((aSocket) =>
          aSocket.send(`${socket.nickname}: ${message.payload}`)
        );
        break;
      case "nickname":
        socket["nickname"] = message.payload;
        break;
    }
  });
});
```

<br>

![image](https://user-images.githubusercontent.com/102353910/163005716-ed1723b9-f626-40f7-8762-6a32e176ae77.png)

<br>

> ##### object로 보내면 안되는 이유
>
> - 연결하고 싶은 front-end와 back-end 서버가 자바스크립트 서버가 아닐수도 있기 때문.
> - 자바스크립트에서 만들었지만 접속하려는 서버가 자바서버이거나, go서버일수도 있기 때문에 string으로 보내야한다.
> - 백엔드에서 다양한 프로그래밍 언어를 사용할 수 있기 때문에 string으로 보내야한다.
> - WebSocket이 브라우저에 있는 API이기 때문이다.

<br>
이렇게 해서 서로 다른 브라우저에서 닉네임도 설정하고 메세지를 주고받을 수 있게 되었다.

<br><br><br><br>
