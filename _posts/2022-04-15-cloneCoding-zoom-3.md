---
title: "[WebRTC] Nomad Coders 줌 클론코딩 #3"
published: true
categories:
  - zoomClone
---

## Video Chat

<br>

지난 시간에 이어서 비디오채팅 기능 만들기

1.  사용자로부터 비디오를 가져와서 화면에 보여주기
2.  마이크 온/오프, 카메라 온/오프 버튼 만들기
3.  카메라 목록 가져오기

<br>

### 1. 비디오 화면에 보여주기

##### home.pug

```html
div#call div#myStream video#myFace(autoplay,playsinLine, width="400",
height="400") button#mute Mute button#camera Turn Camera Off
```

<br>

_💫playsinLine : 모바일 브라우저가 필요로 하는 property.<br>보통 모바일에서 동영상을 재생하면 비디오플레이어를 실행하면서 전체화면이 된다.<br>비디오를 전체화면이 되지 않게 웹사이트에서만 실행되게 해준다._

<br>

##### app.js

```js
const socket = io();

const myFace = document.getElementById("myFace");

let myStream;

async function getMedia() {
  try {
    myStream = await navigator.mediaDevices.getUserMedia({
      audio: true,
      video: true,
    });
    myFace.srcObject = myStream;
  } catch (e) {
    console.log(e);
  }
}

getMedia();
```

<br>

![image](https://user-images.githubusercontent.com/102353910/163557101-356f2f0e-31f8-4924-999e-2757ad47df71.png)

<br>

> ##### 💫 [MediaDevices.getUserMedia()](https://developer.mozilla.org/ko/docs/Web/API/MediaDevices/getUserMedia)
>
> 사용자에게 미디어 입력 장치 사용 권한을 요청하고, 사용자가 수락하면 요청한 미디어 종류의 트랙을 포함한
> `MediaStream` 을 반환한다.

<br><br>

### 2. 버튼 만들기

##### app.js

```js
function handleMuteClick() {
  if (!muted) {
    muteBtn.innerText = "Unmute";
    muted = true;
  } else {
    muteBtn.innerText = "Mute";
    muted = false;
  }
}

function handleCameraClick() {
  if (cameraOff) {
    cameraBtn.innerText = "Turn Camera Off";
    cameraOff = false;
  } else {
    cameraBtn.innerText = "Turn Camera On";
    cameraOff = true;
  }
}

muteBtn.addEventListener("click", handleMuteClick);
cameraBtn.addEventListener("click", handleCameraClick);
```

<br>

위 코드에서 `console.log(myStream.getAudioTracks());` 를 해보면

<br>

![image](https://user-images.githubusercontent.com/102353910/163557932-6541763d-3141-4dac-9952-444232492b61.png)

<br>

위와 같은 배열을 얻을 수 있다. <br> 여기서 Enabled 값을 바꿔주면 mute가 된다.

<br>

##### app.js

```js
function handleMuteClick() {
  myStream
    .getAudioTracks()
    .forEach((track) => (track.enabled = !track.enabled));
  if (!muted) {
    muteBtn.innerText = "Unmute";
    muted = true;
  } else {
    muteBtn.innerText = "Mute";
    muted = false;
  }
}

function handleCameraClick() {
  myStream
    .getVideoTracks()
    .forEach((track) => (track.enabled = !track.enabled));
  if (cameraOff) {
    cameraBtn.innerText = "Turn Camera Off";
    cameraOff = false;
  } else {
    cameraBtn.innerText = "Turn Camera On";
    cameraOff = true;
  }
}

muteBtn.addEventListener("click", handleMuteClick);
cameraBtn.addEventListener("click", handleCameraClick);
```

<br>

### 3. 카메라 목록 가져오기

> ##### 💫 [MediaDevices.enumerateDevices()](https://developer.mozilla.org/ko/docs/Web/API/MediaDevices/enumerateDevices)
>
> 사용 또는 접근이 가능한 미디어 입력장치나 출력장치들의 리스트를 가져온다. 이 메서드는 `Promise` 를 반환한다.

<br>

```js
async function getCameras() {
  try {
    const devices = await navigator.mediaDevices.enumerateDevices();
    console.log(devices);
  } catch (e) {
    console.log(e);
  }
}
```

<br>

![image](https://user-images.githubusercontent.com/102353910/163559208-41d1230c-850b-4e1a-ab03-8cf445a7c280.png)

<br>

유저가 가진 장치 목록을 모두 볼 수 있음(오디오, 비디오, 모니터)<br>비디오 목록을 얻기 위해 'videoinput' 을 가져오면 된다.

<br>

```js
const cameras = devices.filter((device) => device.kind === "videoinput");
console.log(cameras);
```

<br>

![image](https://user-images.githubusercontent.com/102353910/163559482-51383fc8-5316-48b8-8781-70b4b2c8cad4.png)

<br>

장치들 중에 비디오만 콘솔에 출력된다.<br>이제 비디오 id를 가져와서 실제로 영상을 바꿀 수 있도록 기능을 만들자

<br>

##### app.js

```js
async function getMedia(deviceId) {
  const initialConstrains = {
    audio: true,
    video: { facingMode: "user" },
  };
  const cameraConstraints = {
    audio: true,
    video: {
      deviceId: {
        exact: deviceId,
      },
    },
  };
  try {
    myStream = await navigator.mediaDevices.getUserMedia(
      deviceId ? cameraConstraints : initialConstrains
    );
    myFace.srcObject = myStream;
    if (!deviceId) {
      await getCameras();
    }
  } catch (e) {
    console.log(e);
  }
}
```

<br>

이렇게만 해주면 실제로 카메라를 바꿨을 때 바뀌지 않는다.<br>`console.log(myStream.getVideoTracks());` 를 해보면 현재 선택된 카메라가 무엇인지 콘솔에서 확인할 수 있다.<br>getCameras()에서 업데이트해준다.

<br>

```js
async function getCameras() {
  try {
    const devices = await navigator.mediaDevices.enumerateDevices();
    const cameras = devices.filter((device) => device.kind === "videoinput");
    const currentCamera = myStream.getVideoTracks()[0];
    cameras.forEach((camera) => {
      const option = document.createElement("option");
      option.value = camera.deviceId;
      option.innerText = camera.label;
      if (currentCamera.label == camera.label) {
        option.selected = true;
      }
      cameraSelect.appendChild(option);
    });
  } catch (e) {
    console.log(e);
  }
}
```

<br><br><br><br>

## WebRTC

#### (Web Real-Time Communication)

실시간 커뮤니케이션을 가능하게 해주는 `peer-to-peer` 기술이다.

<br>

Socket.io는 peer-to-peer가 아니다.<br>왜냐하면 한 서버에 많은 web socket들이 연결되어 있기 때문이다.<br>메세지를 보내면 메세지는 web socket에서 서버로 보내진다.<br>모두가 그 서버에 연결되어있고 서버는 모두에게 메세지를 전달하는 역할이다.<br>Socket.io에서는 언제나 서버를 이용해야만 메세지를 보낼 수 있다.<br>사실 다른 사람에게 메세지를 보내는 것이 아니라 서버에게 메세지를 보내면 그 서버가 해당 유저에게 메세지를 전달하는 것이다.

<br>

peer to peer는 비디오/오디오/텍스트가 서버로 가는 게 아니라 직접 다른 유저에게로 간다.<br>내 브라우저가 상대방의 브라우저에 직접 연결되기 때문에 속도도 빠른 것이다.<br>물론 서버가 전혀 필요하지 않은 것은 아니다.<br>오디오나 영상을 전송하기 위한 서버가 아니라 signaling 이라는 것을 하기 위해 필요하다.<br>signaling이 끝나면 peer-to-peer 연결이 된다.<br>브라우저가 서버에게 conofiguration과 브라우저의 위치같은 정보만 전달한다.<br>서버는 영상이나 비디오 등의 메세지는 처리하지 않는다.

<br><br><br>

### peer-to-peer

![image](https://user-images.githubusercontent.com/102353910/163564090-f0b3d56e-3715-41a6-8bc9-d11c39f4b430.png)

<br>

위와 같은 과정으로 peer-to-peer connection을 만들어 줄 수 있다.<br><br>우선 peerConnection을 각 브라우저에 만들어준다.

<br>

![image](https://user-images.githubusercontent.com/102353910/163565440-9c3c04ab-6cad-4cfc-8d85-5856598d3d02.png)

<br>

영상과 오디오를 연결을 통해 전달해야한다.<br>peer-to-peer 연결 안에 영상과 오디오를 집어넣어야한다.<br>`myStream.getTracks()` 로 콘솔에서 내 마이크와 비디오 트랙을 볼 수 있다.<br>이 트랙들을 stream에 추가하면 된다.

<br>

```js
function makeConnection() {
  myPeerConnection = new RTCPeerConnection();
  myStream
    .getTracks()
    .forEach((track) => myPeerConnection.addTrack(track, myStream));
}
```

<br><br><br>

이제 `offer` 를 만들어서 다른 사람이 참가할 수 있도록 초대장을 만든다.<br>우리가 누구이며 어디에 있고 그런 것들을 설명하는 것이다.<br>그리고 offer를 다른 브라우저에 보내야 한다.<br>어떤 방이 offer를 보내는지 방 이름도 알려준다.

<br><br>

##### app.js

```js
socket.on("welcome", async () => {
  const offer = await myPeerConnection.createOffer();
  myPeerConnection.setLocalDescription(offer);
  socket.emit("offer", offer, roomName);
});

socket.on("offer", (offer) => {
  myPeerConnection.setRemoteDescription(offer);
});
```

<br>

##### server.js

```js
io.on("connection", (socket) => {
  socket.on("offer", (offer, roomName) => {
    socket.to(roomName).emit("offer", offer);
  });
});
```

<br>

> ##### 💫 [setRemoteDescription()](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/setRemoteDescription)
>
> signaling서버를 통해 다른 peer로부터 제안이나 응답을 받은 후에 호출된다.
> 니꼬쌤은 'offer는 나중에 접속한 브라우저'라고 했다.

<br><br>

![image](https://user-images.githubusercontent.com/102353910/163568424-0db082a1-05ca-463b-b5d4-31557d231adb.png)

<br>

a가 먼저 방에 참가하고 b가 참가하면 handelWelcomeSubmit()의 `socket.emit("join_room", input.value, startMedia);` 부분을 서버로 보내는데 <br>그러면 서버가 a에게 알려주고 a는 offer를 전송한다.<br> offer는 b로 돌아오는데 offer가 도착한 순간 너무 빨라서 myPeerConnection은 아직 존재 하지조차 않는 상태이기 때문에 위와 같은 에러가 나온다.<br>왜냐하면 welcome코드는 b에서 아직 발현되지 않았기 때문이다.<br>media를 가져가서 연결을 만들어주는 startMedia함수를 방에 참가하기 전에 호출해줘야한다.

<br><br><br>

#### iceCandidate

iceCandidate는 인터넷 연결 생성이다.<br>브라우저가 서로 소통할 수 있게 해주는 방법이다.<br>connection이 일어나는 동시에 iceCandidate도 동작한다.<br>iceCandidate를 받으면 상대방의 네트워크 정보를 추가하고 서로 화면에 카메라 영상을 보이게 한다.

<br>

##### home.pug

```html
video#peersFace(autoplay,playsinLine, width="400", height="400")
```

##### add.js

```js
function handleAddStream(data) {
  const peersFace = document.getElementById("peersFace");
  peersFace.srcObject = data.stream;
}
```

<br>

상대 비디오를 담아줄 공간을 만들고 다른 브라우저에서 실행하면 카메라가 잘 나온다.

<br>

![image](https://user-images.githubusercontent.com/102353910/163571097-494efee8-cd9d-475d-afb9-31f40d7cc13a.png)

<br><br>

![image](https://user-images.githubusercontent.com/102353910/163571123-86aacda3-45d2-4467-ab1b-de6cae15335b.png)

<br>카메라 켜고 끄는것도 잘 작동한다.<br>하지만 카메라를 바꾸는 것은 작동이 잘 안된다고 한다.<br>나는 카메라가 하나밖에 없어서 모르겠지만 일단 니꼬쌤 따라 쳤다.

<br><br>

peer연결을 만드는 동시에 그 연결에 track을 추가했었는데, track을 바꿔주면 된다.<br>카메라를 바꿀 때 마다 서로 다른 id로 새로운 stream을 만들고 있는데, peer에게 줄 stream을 업데이트 하면 된다.
<br>

```js
function makeConnection() {
  myPeerConnection = new RTCPeerConnection();
  myPeerConnection.addEventListener("icecandidate", handleIce);
  myPeerConnection.addEventListener("addstream", handleAddStream);
  myStream
    .getTracks()
    .forEach((track) => myPeerConnection.addTrack(track, myStream));
}

async function handleCameraChange() {
  await getMedia(cameraSelect.value);
  if (myPeerConnection) {
    const videoTrack = myStream.getVideoTracks()[0];
    const videoSender = myPeerConnection
      .getSenders()
      .find((sender) => sender.track.kind === "video");
    videoSender.replaceTrack(videoTrack);
  }
}
```

<br><br><br>

폰에서도 테스트해주기 위해 로컬터널을 설치해줬다.

<br>

    $ npm i localtunnel
    $ lt --port 3003

<br>

주소를 받아서 핸드폰으로 들어가보니까 후면카메라도 다 잘 나온다.

<br>

![image](https://user-images.githubusercontent.com/102353910/163572029-e8e519de-e526-4c00-82e1-f676ab0a1a74.png)

<br><br>

사실 같은 와이파이 연결이 되어있기 때문에 잘 나오는거라고 한다.<br> 같은 와이파이가 아니면 stream이 나오지 않는단다.<br> 그 이유는 `stun서버` 가 필요하기 때문이다.<br>컴퓨터가 공용 ip주소를 찾게 해주는 것이다.<br>전문적으로 하려면 직접 만들어야한다고 한다.<br>테스트 용도로 사용하려면 구글이 무료로 제공하는 서버를 이용할 수 있다고 한다.

<br><br><br>

#### ✅ 더 살펴볼 것 : Data Channel

peer-to-peer 유저가 언제든지 모든 종류의 데이터를 주고받을 수 있는 채널이다.<br>이미지, 파일, 텍스트, 게임 업데이트 패킷 같은 것들도 모두 주고받을 수 있다.<br>Socket.io없이도 채팅을 만들 수 있다.
<br><br>

#### ❌WebRTC를 쓰면 안되는 상황

너무 많은 peer를 가질 때 => 느려진다.<br>같은 비디오 스트림을 여러명에게 보내게 되기 때문이다.<br>대신해서 어떤 회사들은 SFU라는 것을 사용한다고 한다. <br>peer-to-peer와는 다르게 모두로부터 스트림을 받아서 압축하는 방식이라고 한다.

<br><br><br><br>

### ⚡코드

<script src="https://gist.github.com/seulgi9506/690a076c64230792ad751b6b87949403.js"></script>

<br><br><br><br>
