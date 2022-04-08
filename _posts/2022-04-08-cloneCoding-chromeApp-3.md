---
title: "[Vanilla JS] Nomad Coders 바닐라 JS로 크롬 앱 만들기 #3"
published: true
categories:
  - Momentum
---

## HTML & Javascript

<br>

![image](https://user-images.githubusercontent.com/102353910/162368600-b8ba29d7-c5bb-4f3d-99e2-9a1e255f778d.png)
![image](https://user-images.githubusercontent.com/102353910/162368740-353f60f0-5870-4a12-9959-66ed20b32b4d.png)

<br>

HTML과 Javascript는 서로 연결되어있다.<br>콘솔창을 열어 간단한 js 코드를 실행해보면 알 수있다. <br><br>콘솔창에 document.title = "boom" 을 입력하고 실행시키면 즉시 브라우저 탭의 타이틀이 변경되는 것을 볼 수 있다.<br>그리고 개발자 창 elements탭의 `<title>`태그도 변경된 것을 확인할 수 있다.<br>이 것이 바로 HTML과 Javascript가 연결되어있다는 증거다.<br>그리고 우리는 Javascript을 이용해서 HTML의 모든 요소들을 바꿀 수 있다.

<br><br><br><br>

## HTML의 요소 가져오기

<br>
우리는 Javascript를 이용해서 HTML의 모든 요소들을 바꿀 수 있다.<br>그러려면 Javascript에 HTML의 어느 부분을 바꾸고 싶은지 알려줘야 한다.<br>

![image](https://user-images.githubusercontent.com/102353910/162367027-c69a9aa0-bb09-430a-b615-0c249889ccad.png)

<br>console창에 document를 입력하면 html코드가 나오는 것을 확인할 수 있다. <br>그리고 console.dir(document) 를 입력하면 html의 요소들이 객체형태로 들어있는 것을 확인할 수 있다. <br>그래서 우리가 바로 위에서 document.title로 타이틀을 변경할 수 있었던 것이다.
<br>
![image](https://user-images.githubusercontent.com/102353910/162369124-5e158d47-fc6f-4ed7-9a92-f1fc5ac595f4.png)

<br>

document 객체의 key로 요소를 찾을 수 있고 그 value를 바꿀 수 있다.<br>
**<mark style="background-color: #d4d4f8">document.getElementById("id")</mark>** : 태그의 id 명으로 요소 가져오기<br>
**<mark style="background-color: #d4d4f8">document.getElementsByClassName("class")</mark>** : 태그의 class 명으로 요소 가져오기<br>
**<mark style="background-color: #d4d4f8">document.getElementsByTagName("tag")</mark>** : 태그 명으로 요소 가져오기<br>
**<mark style="background-color: #d4d4f8">document.querySelector(".class tag")</mark>** : CSS방식으로 요소 가져오기(가장 먼저 찾은 하나의 요소만을 가져온다)<br>
**<mark style="background-color: #d4d4f8">document.querySelectorAll(".class tag")</mark>** : CSS방식으로 요소 가져오기(동일 조건의 모든 요소들을 가져온다)<br>

<br><br><br><br>

## Events

<br>
![image](https://user-images.githubusercontent.com/102353910/162370656-38507d14-d3b6-4294-8b80-e085c74c0c0e.png)

<br>요소들을 다시 console.dir로 요소들의 내부를 자세히 확인할 수 있는데, <br>위 사진처럼 on어쩌구 하는 것들이 엄청 많이 들어있다.<br>이 on어쩌구들은 모두 event인데 event는 사용자가 행동하는 것들을 가르킨다. <br>예를 들어 마우스를 올리거나, 마우스로 클릭하거나, 복사하거나, 윈도우 크기를 조절한다던가 하는 것들이다.<br><br>우리는 이런 사용자의 행동에 따라서도 웹페이지를 바뀌게 만들 수 있다.<br>사용자가 마우스를 클릭했을때 색이 변하게 한다던지, 마우스를 올렸을 때 모양이 바뀌게 한다던지 하는 것들이다.<br><br>
바로바로 **<mark style="background-color: #d4d4f8">addEventListener</mark>** 를 통해서 바꿀 수 있다.<br>아래 click me를 클릭해보자 !<br>

<iframe src="https://codesandbox.io/embed/jolly-nash-b6jn5h?autoresize=1&fontsize=14&moduleview=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="jolly-nash-b6jn5h"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<br>

요소를 가져와서 사용자가 행동했을 때 어떻게 반응할지 함수로 만들어주고,<br>addEventListenr로 어떤 상황에서 반응할지를 알려주면 된다.<br><br>이런 것도 할 수 있다.<br>

<iframe src="https://codesandbox.io/embed/charming-dawn-k0kmeb?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="charming-dawn-k0kmeb"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<br>사용자가 클릭하면 텍스트 색을 바꾸고 다시 클릭하면 원래대로 바꾸기.<br>그런데 이제 `classList` 라는 것을 사용하면 더 쉽게 바꿀 수 있다.

    function  handleTitleClick() {
        const clickedClass = "clicked";
        if (h1.classList.contains(clickedClass)) {
    	    h1.classList.remove(clickedClass);
        } else {
    	    h1.classList.add(clickedClass);
        }
        h1.style.color = newColor;
    }

위 코드에서 classList는 태그에 있는 클래스 이름들을 확인해서 <br>clicked라는 이름이 있으면 파랑색, 없으면 토마토색으로 바꿔준다.<br>여기까지 듣고 오오,, 꽤 신기한걸,,? 하고 생각했다.<br>하지만 진짜 신기한게 있다.<br><br>

    function  handleTitleClick()  {
        h1.classList.toggle("clicked");
    }

바로 **<mark style="background-color: #d4d4f8">toggle</mark>** 이라는 녀석이다. <br>저 녀석 혼자서 저 위에 여러줄의 코드와 같은 기능을 한다는 것이다 ! ! !<br>매우 신기하고 놀라운 녀석이 아닐 수 없다.<br>아마 자주 사용하는 기능이니까 저렇게 따로 만들어진 것이 아닐까 추측해본다.<br>만약 니꼬쌤이 알려주지 않았더라면,, 나는 저 바보같은 여러줄의 코드를 만들고 있었을지 모른다.
<br><br>그리고 사용 가능한 엄청나게 많은 이벤트들이 있는데 그것은 구글에 [event mdn](https://developer.mozilla.org/ko/docs/Web/Events) 이라고 검색하면 찾을 수 있다.

<br><br><br><br>
