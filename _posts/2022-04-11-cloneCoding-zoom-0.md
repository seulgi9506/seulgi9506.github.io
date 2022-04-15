---
title: "[Setup] Nomad Coders 줌 클론코딩 #0"
published: true
categories:
  - zoomClone
---

## Setup

<br>

<script src="https://gist.github.com/seulgi9506/721b7b101d8d1c55f0b05675ac28e17e.js"></script>

<br><br>

#### **<mark style="background-color: #d4d4f8">"presets": ["@babel/preset-env"]</mark>**<br>

사실 bebel은 그 자체로는 아무것도 하지 않는다.<br>진짜 동작하는 것은 **babel plugin**이다.<br>babel이 무엇을 하게 하려면 plugin을 설치해야하고, plugin은 npm 라이브러리를 가지고 있다.<br>그래서 설치하고 싶은 각각의 plugin을 위해 새로운 npm 라이브러리를 설치하거나 또는 preset을 사용할 수 있다.<br>babel foundation에서 제공하는 공식 preset이 있는데, plugin 번들 파일을 포함한 preset이다.<br>(이 말인 즉슨 npm 설치와 babel설정을 한 번만 하면 plugin들이 자동적으로 설치된다는 뜻이라고 한다.)<br>기본적으로 babel-preset-env는 단순히 모둔 ES6 plugin을 설치한다.<br>하지만 이 것은 컴파일된 자바스크립트의 양이 많아지기 때문에 코드를 길어지게 만든다.<br>따라서 원하는 브라우저만 지원 가능하도록 plugin을 선택할 수도 있다.<br>

> [👉참조 : \[번역\] babel-preset-env는 무엇이고 왜
> 필요한가?](https://velog.io/@pop8682/%EB%B2%88%EC%97%AD-%EC%99%9C-babel-preset%EC%9D%B4-%ED%95%84%EC%9A%94%ED%95%98%EA%B3%A0-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%9C%EA%B0%80-yhk03drm7q)

<br><br>

#### **<mark style="background-color: #d4d4f8">"ignore": ["src/public/*"]</mark>**<br>

nodemon이 파일이 수정될 때마다 서버를 재시작해주고 있는데 재시작 대상에서 제외하기 위한 코드를 추가해줬다.<br>scr/public에 있는 모든파일(\*)을 제외했다.<br>**nodemon --ignore "무시할 파일"** 로도 동일하게 설정해 줄 수 있다.

<br><br>

#### **<mark style="background-color: #d4d4f8">app.get("/\*", (req, res) => res.redirect("/"));</mark>** <br>

catch url<br>유저가 어떤 url로 접속을 시도하던지 무조건 home으로 돌려보내줌.

<br><br><br><br>

## recap

<br>

nodemon 이 프로젝트를 지켜보다가 변경사항이 있으면 자동으로 서버를 재시작해준다.<br>서버를 재시작 하는 대신 babel-node를 실행한다.<br>babel은 우리가 작성한 코드를 일반 node.js 코드로 컴파일해주는데, 그 작업을 src/server.js에서 해준다.

<br><br><br><br>
