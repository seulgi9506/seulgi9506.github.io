---
title: "todo project daily log - 1 "

published: true

categories:
  - minitodo
---

📑 todo project daily log - 1
{: .notice--primary}

<br><br><br>

죽이 되든 밥이 되든 무서워서 시도도 안하면 아무것도 안되니까 일단 시작하자! 라는 생각으로 미뤄왔던 미니프로젝트를 시작한다.
나는 할 수 있다!!!!!!!!!

<br>

우선 내가 만드는 투두에 데이터베이스가 필요할 것 같다는 생각이 들었다.<br>Js와 데이터베이스 연결.. 이거 node.js랑 mongoDB연결하면 되지 않나? 하는 생각부터 든다.<br>하지만 난 몽고디비는 사용해 본 적이 없다.<br>오라클과 mysql은 사용해봤다.<br>얼마전에 친구와 미니프로젝트를 하려고 node에 오라클을 연결하는데 하루를 몽땅 투자했는데, 정말 머리아프고 어려웠던 경험이 있다…<br>그렇다면 mysql을 연결하는 것은 어떨까

<br>

아니아니 근데 이제 연결하기전에 테이블을 어떻게 만들건지 데이터베이스 먼저 구상해야하지 않을까?

<br>

일단 내가 만들고 싶은건,<br>

- 달력 : 주간/월간 달력으로 할 일 표시
- 할 일 : 할 일은 그룹으로 묶을 수 있고 기간을 설정할 수 있다.(기간 설정하지 않을 시에는 작성일로 등록). <br>할 일 별로 중요도를 표시할 수 있다.(별⭐모양으로 표시)
- 오늘 : 메인화면에서 오늘 할 일들을 리스트로 확인 가능(중요도가 높은 일이 위로 배치).
- 그룹별 할 일 : 그룹으로 나눠진 할 일들을 확인 가능.(이건 달력에서도 되면 좋겠다.)

<br>

이정도 .. ? <br>사실 처음에는 데이터베이스를 사용하지 않고 로컬스토리지로 간단히 해보려고 했는데, 하다보니 욕심이 생겨서 데이터베이스를 만들기로 했다.<br>하면서 추가될 수도 있겠지만 일단 이 정도로 구상했다.

그렇다면 테이블을 한 번 만들어보자.

<br><br><br><br>

## 🚨 [ERROR] Mysql root 비밀번호

<br><br>

테이블을 만들기 전부터 난관에 봉착했다.<br>MySQL 워크벤치를 이용하려고 했는데 root 비밀번호를 까먹어서 로그인이 안되는 것 같다.

<br>

![image](https://user-images.githubusercontent.com/102353910/167777177-a3340087-7297-40e6-b130-f3a4fbc9d147.png)

<br>

이거 분명히 구글링하면 방법이 있을테지.<br>나만 이렇게 비밀번호를 잊어먹거나 하는게 아닐테야.

<br><br><br>

> ### 👉 참고 블로그 : [Windows MySQL root 비밀번호 변경하기](https://one-step-a-day.tistory.com/141)
>
> 1. 작업관리자에서 MySQL 종료
> 2. 관리자 권한으로 cmd 실행 -> MySQL이 설치된 경로로 이동<br>`where mysql`을 입력하면 경로를 알아낼 수 있다.
> 3. 이동한 경로에서 <br>`mysqld.exe --skip-grant-tables --console --shared-memory` 를 입력

<br><br><br>

![image](https://user-images.githubusercontent.com/102353910/167777721-f1cdd882-302c-40a6-8f57-caa5483435cf.png)

<br>

![image](https://user-images.githubusercontent.com/102353910/167777749-f0418aaf-7a99-476f-972d-9fa3fe1e3da4.png)

<br><br><br>

에러가 발생했는데, 참고한 블로그에도 같은 에러가 보인다.<br>침착하게 따라해본다.<br>`mysqld --initialize --console` 입력하고 다시 실행

<br><br><br>

![image](https://user-images.githubusercontent.com/102353910/167777949-a4a22381-45c5-4ae2-989b-ececd90115c5.png)

<br>

하지만 이 녀석은 참고 블로그 주인장네 컴퓨터와는 다른 답변을 내놓았다.<br>청개구리같은녀석..

<br><br><br>

다시 구글링해보며 이것 저것 따라해 봤지만 해결되지 않았다..

> ##### 참고 페이지
>
> [Can't create test file lower test start server mysql](https://stackoverflow.com/questions/41504580/cant-create-test-file-lower-test-start-server-mysql)<br> > [mysql my-013276 error / window 10](https://cleancode-ws.tistory.com/99)

<br><br><br>

결국 MySQL을 삭제하고 재설치해서 정신개조 시켜줬따.

<br>

> ### 👉 참고 : [MySQL 삭제 완벽하게 하기](https://allhpy35.tistory.com/53)
>
> 1. 제어판에서 MySQL 어쩌구 하는 프로그램들을 모두 삭제
> 2. 아래의 폴더들 모두 삭제<br>C:\Program Files\MySQL<br>C:\Program Files (x86)\MySQL<br>C:\ProgramData\MySQL
> 3. 재설치

<br><br>

재설치 해주고 root 비밀번호는 소중히 메모장에 메모해뒀다.^-^

<br><br><br><br>

## 🚨 [ERROR] MySQL auto_increment

<br><br>

이제 구상하면서 대충 테이블을 만들어봤는데 또 에러가 나와부렀다.

<br>

> Incorrect table definition; there can be only one auto column and it must be defined as a key

<br>

![image](https://user-images.githubusercontent.com/102353910/167780749-30ec3e33-00a0-4ac9-a6d4-ac17becb508c.png)

<br>

관련해서 구글링해보니 auto_increment를 사용한 경우 항상 primary key로 지정되어야 한다고 한다.<br>하지만 나는 auto_increment를 사용한 u_no가 아닌 u_id를 기본키로 사용하고 싶었다.<br>그리고 not null 속성을 주면 오류를 발생시킬 수 있다고 한다.

<br>

> ##### 👉 참고 : [auto_increment를 사용할 때 주의할 점](https://blog.daum.net/question0921/539)

<br>

그래서 not null 속성도 빼고 u_no와 u_id 두 개 모두 기본키로 해서 테이블을 만들었다.<br>첫 번째 테이블은 만들어졌다.<br>근데 두 번째 테이블이 안만들어진다.<br>이거는 아무리 구글링을 해도 잘 이해를 못하겠다.

<br>

![image](https://user-images.githubusercontent.com/102353910/167782174-746f628a-62df-4054-897b-3599d52405e9.png)

<br><br><br>
