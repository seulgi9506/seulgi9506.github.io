---
title: "[Vanilla JS] Nomad Coders 바닐라 JS로 크롬 앱 만들기 #8"
published: true
categories:
  - Momentum
---

## Weather info

<br>

### weather.js<br>

<br>

```js
const API_KEY = "myOwnApiKey";

function onGeoOk(position) {
  const lat = position.coords.latitude;
  const lon = position.coords.longitude;
  const url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`;
  fetch(url)
    .then((response) => response.json())
    .then((data) => {
      const weather = document.querySelector("#weather span:first-child");
      const city = document.querySelector("#weather span:last-child");
      city.innerText = data.name;
      weather.innerText = `${data.weather[0].main} / ${data.main.temp}`;
    });
}

function onGeoError() {
  alert("Can't find you. No weather for you.");
}

navigator.geolocation.getCurrentPosition(onGeoOk, onGeoError);
```

<br>

**<mark style="background-color: #d4d4f8">navigator.geolocation</mark>** 을 이용하면 웹에서 장치의 위치를 알아낼 수 있다.<br>👉[참고](https://developer.mozilla.org/ko/docs/Web/API/Geolocation_API/Using_the_Geolocation_API)<br><br>getCurrentPosition()의 괄호 안에 성공했을 때 실행할 함수를 먼저 써주고 실패했을 때 실행할 함수를 뒤에 써준다.<br>성공했을 때 js가 전달해주는 위치를 console.log로 확인해보면 아래와 같은 값들을 콘솔에서 확인할 수 있다.

<br>

![image](https://user-images.githubusercontent.com/102353910/162575609-2b38c4c3-adb8-4639-89f7-e4b68365c19e.png)

<br>

여기서 우리가 주목해야할 값은 <mark style="background-color: #f2ea6e">latitude(위도)</mark>와 <mark style="background-color: #f2ea6e">longitude(경도)</mark>이다.<br>이후에 사용할 openweathermap API에서 필요하니 각 위도와 경도를 lat과 lon으로 저장해뒀다.<br>
<br>

### OpenWeather API

<br>

👉[OpenWeather API](https://openweathermap.org/) 에서 위치별 날씨에 대한 정보를 무료로 사용할 수 있다.<br><br>![image](https://user-images.githubusercontent.com/102353910/162575791-a5e79efa-59d0-461c-98de-5e66c67d6b4b.png)

<br><br>여기에서 날짜 정보에 접근할 수 있는 각자 개인 API Key를 얻을 수 있으니 회원가입을 먼저 해주자<br>그리고 API 탭에 들어가서 Current Weather Data의 `API Doc`을 누르면 API를 사용할 수 있는 url이 나온다.<br><br>
![image](https://user-images.githubusercontent.com/102353910/162575918-bc8b7fce-ee49-4363-8753-ceb2c06c56c5.png)
<br><br>

API call 부분의 주소를 복사해서 주소창에 입력 해보자<br>
lat과 lon은 아까 getCurrentPosition에서 얻은 위도와 경도 값,<br>그리고 API key는 사이트에 로그인한 뒤 My API keys에서 가져올 수 있다.<br><br>

![image](https://user-images.githubusercontent.com/102353910/162576114-e6bbb911-fdfe-4177-bba0-b7b70eb39bef.png)

<br><br> 그리고 나면 위 사진처럼 알 수 없는 것을 볼 수 있는데 <br>자세히 보면 현재 위치와 온도, 날씨 등을 알려주고 있다. <br>다만 온도 수치가 조금 이상한데 그것은 화씨로 표시해주고 있기 때문이다. <br>우리에게 익숙한 섭씨로 온도를 받으려면 해당 url 뒷 부분에 <mark style="background-color: #f2ea6e"> &units=metric</mark>을 붙여주면 섭씨로 변한다.
<br><br>
그리고 나서 API를 사용하기 위해 <mark style="background-color: #d4d4f8">fetch()</mark>함수를 이용해 아까 url을 주소창에 입력했을 때 확인했던 json객체를 받아온다.<br>받아온 json에서 위치와 날씨 정보를 찾아 각 html태그 요소에 넣어준다.

<br><br><br><br>

##### 여기까지 수행한 결과물

<br>

![image](https://user-images.githubusercontent.com/102353910/162575097-9b96323b-5438-4897-a39d-a54704b5b51d.png)

<br><br><br><br>

여기에서 강의는 끝이났다.<br>이제 직접 꾸며서 레파지토리에 업로드해야겠다.
