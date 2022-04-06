---
title: "[Node.js 기초] Inflearn 한입 크기로 잘라먹는 리액트 #3 "
published: true
categories:
  - winterlood-react
---

## Node.js 란?

![image](https://user-images.githubusercontent.com/102353910/161737275-4ab2e9fb-bbde-4caa-af07-7f2810a7099b.png)<br><br>

자바스크립트를 웹 브라우저 외에 다른 곳에서도 사용할 수 있도록 만든 도구<br>Node.js = 자바스크립트의 실행환경 = Javascript's Runtime<br>브라우저 없이 자바스크립트를 컴퓨터에서 실행할 수 있다.<br>카카오톡, 파워포인트 등의 PC프로그램을 만들 수 있다. <br>JS로 웹서버까지 만들 수 있게 되었다. <br><br>

#### React.js와의 관계

React.js = 브라우저에서 동작하는 복잡하고 여러가지 기능을 가진 js파일을 쉽게 만들어내는 기술<br>React에서 만들어낸 js파일들은 마치 프로그램처럼 돌아간다. <br> => 리액트로 만든 웹사이트를 웹 어플리케이션 / 리액트 어플리케이션 이라고 부른다.<br>Node.js를 기반으로 사용할 수 있는 기술이며 Node.js 없이는 사용하기 어렵다.
<br><br><br><br>

## NPM : Node Package Manager

<br>
Node.js를 사용하면서 다른 사람들이 만들어 놓은 모듈을 다운받아서 사용할 수 있게 해주며, 개발할 프로젝트를 관리하는 데에도 도움을 준다.<br><br>
![image](https://user-images.githubusercontent.com/102353910/161738217-3b807ebe-ef8f-4429-bd53-75f79674702a.png)<br><br>
구글에 'npmjs'로 검색하면 무료로 사용할 수 있는 npm 모듈들을 모아놓은 사이트를 찾을 수 있다. → [npm](https://www.npmjs.com/)<br>

<br><br><br><br>

## npm 사용해보기

<br>

![image](https://user-images.githubusercontent.com/102353910/161738986-fc60d861-aa10-4f55-967b-e0d9a9cb9140.png)<br>
<br>터미널에 다음 명령어를 입력하여 npm 프로젝트를 생성해준다.<br>

    npm init

<br><br><br>

![image](https://user-images.githubusercontent.com/102353910/161739331-782a5560-8e9f-4b9e-b5d5-54f626f624be.png)<br>
<br>맨 처음에 나오는 package name만 설정해주고 나머지는 다 엔터<br>마지막에 yes를 입력하면 왼쪽 explorer에 'package.json'이 생성된다.<br><br><br><br>
![image](https://user-images.githubusercontent.com/102353910/161739502-2b36c40d-9dc8-47d0-8fe8-60491a0b6975.png)<br>
<br>'package.json'파일에 'start'라는 키워드로 실행 명령어를 입력했다.<br>자주 실행하는 긴 명령어들을 키워드로 등록할 수 있다.<br><br><br><br>
![image](https://user-images.githubusercontent.com/102353910/161739774-a3618af3-44c4-4c43-8a3b-d886f7c8b29b.png)<br>
<br>npmjs.com에서 'randomcolor'라는 모듈을 찾아 설치해봤다.<br>오른쪽에 보이는 intall 안의 ' npm install randomcolor'라는 명령어를 터미널에 입력해주면 설치가 완료된다.<br><br><br><br>
![image](https://user-images.githubusercontent.com/102353910/161740109-5d4929e3-c0bb-4178-9401-2986f148fe88.png)<br>
<br>설치가 완료되고 나면 못보던 파일들이 생성된것이 보이는데<br><mark style="background-color: #d4d4f8">node_modules</mark> : 설치한 외부 패키지들의 코드가 들어있는 보관소<br><mark style="background-color: #d4d4f8">package-lock.json</mark> : 외부 설치된 패키지들이 정확히 어떤 버전으로 설치되었는지 알 수 있는 파일<br><br><br><br>

![image](https://user-images.githubusercontent.com/102353910/161741597-90eb3dc9-0806-4dff-8a00-6da4009c6144.png)<br>
<br>
모듈은 'require'내장함수로 불러올 수 있다. <br>뒤에 경로를 입력해주면 되는데 <br>이런식으로 외부에서 가져온 모듈의 경우 경로를 따로 지정하지 않아도 된다. <br>자동으로 node_modules폴더에서 가져온다.

<br><br><br><br>
