---
title: "[Eclipse] 이클립스에서 리액트 만들기"
published: true
categories:
  - etc
---

📑 이클립스에서 리액트 만드는 방법
{: .notice--primary}

<br><br><br><br>

이클립스를 사용할 수 밖에 없는 상황인데(나는 vscode가 편하다.) <br>리액트를 사용해서 프로젝트를 하고 싶다.<br>그래서 이클립스에서 리액트 프로젝트를 만드는 방법을 알아왔다.

<br><br><br><br>

### 1. 이클립스에서 Marketplace 실행

<br><br>

![image](https://user-images.githubusercontent.com/102353910/169828122-91467e61-e8ad-42a6-8f57-bb203595a43d.png)

<br>

> `Help > Eclipse Marketplace...`

<br><br><br><br>

### 2. 리액트 다운로드

<br><br>

![image](https://user-images.githubusercontent.com/102353910/169828516-dbc61f5d-68e7-4aad-ae30-9dc7f8af3069.png)

<br>

![image](https://user-images.githubusercontent.com/102353910/169828602-98764b30-fa6e-486c-a5fa-98466d67b1d6.png)

<br><br><br><br>

### 3. restart

<br>

리액트 다운로드가 완료되면 restart 알림창이 뜬다.<br>이클립스를 재시작 해준다.

<br><br><br><br>

### 4. 리액트 프로젝트 만들기

<br><br>

![image](https://user-images.githubusercontent.com/102353910/169828889-fdbdcfbe-cd4e-400a-acd1-ecd5ee92b293.png)

<br>

![image](https://user-images.githubusercontent.com/102353910/169828992-df94e93e-4e4e-4749-adef-8240739eb446.png)

<br>

프로젝트를 만들면 일반적으로 포함된 node_modules 폴더가 생기지 않은 것을 확인할 수 있다.

<br><br><br><br>

### 5. node_modules 폴더 만들기

<br><br>

![image](https://user-images.githubusercontent.com/102353910/169829236-c32d0ec9-2d00-4b69-b653-c82b5fe12460.png)

<br>

터미널 열기

<br><br>

![image](https://user-images.githubusercontent.com/102353910/169829322-0a9bd902-cbe3-427c-9b2e-f990f25d7085.png)

<br>

> `npm install`<br>~~(터미널이 왜 이렇게 구리게 생긴지는 알 수 없다.)~~

<br><br>

![image](https://user-images.githubusercontent.com/102353910/169829607-9a2aaffd-76a8-442c-b751-cc1d0c574cc4.png)

<br>

생성 완료

<br><br><br><br>

### 6. create react app

<br>

> `npx create-react-app 프로젝트명`

<br><br><br><br>

### 7. 실행

<br>

터미널에 `npm start`로 실행해도 되고 아래 사진처럼 실행 가능하다.

<br>

![image](https://user-images.githubusercontent.com/102353910/169829945-ff21c778-b767-43b1-9293-dcbaabca396c.png)
