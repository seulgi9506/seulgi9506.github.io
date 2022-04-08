---
title: "[Github] github 프로필을 꾸며보자 !"
published: true
categories:
  - etc
---

# README 만들기

<br><br>

인프런 강의를 들으며 미니프로젝트를 따라 만들고 깃 레파지토리에 업로드하면서 <br>리드미에 프로젝트 설명을 해야겠다는 생각이 들어 리드미 쓰는법을 구글링했는데, <br>깃허브 프로필 꾸미기가 자꾸 나오는 것이 아닌가.. !<br><br>이럴수가.. 나 빼고 모두 예쁜 프로필을 가지고 있었어...<br>그래서 나도 리드미로 내 프로필을 꾸며야지!! 하고 맹글어보았다. 나의 **리.드.미.**<br>👉[참고 공식문서](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/managing-your-profile-readme)
<br><br><br><br>

## Step 1 . Repository 만들기

<br><br>

✅ github 사용자 이름과 동일한 이름으로 repository 만들기<br>
✅ 공개 저장소로 만들기<br>
✅ 'Initialize this repository with: **Add a README file**' 체크 !

<br><br>

![image](https://user-images.githubusercontent.com/102353910/162457628-63f0da34-b560-4f29-bcf2-11ddcf707d27.png)

<br><br>

![image](https://user-images.githubusercontent.com/102353910/162458465-3f664d84-b0bf-4528-850d-658c879b5ded.png)

<br><br>

Edit README 고고

<br><br><br><br>

## Header

<br><br>

그래!! 나도 멋진 프로필을 만들겠어 !!<br>라고 생각하고 다른 블로그를 참고하여 열심히 헤더를 만들었다.<br>**그러나**<br>난 내가 슬기짱이라는거 말고는 별로 쓸게 없다는 점이다...<br>아직 배우는 중인데다 백수이다...<br>하지만 언젠간 저 리드미를 가득 채우고 말리라...

<br><br>

![image](https://user-images.githubusercontent.com/102353910/162467398-e48f0089-3777-4f9a-978b-1137dd9dbea7.png)
가진것에 비해 거창한 프로필.png

<br><br>

> ### 참고⭐
>
> github profile 예쁘게 꾸미기 : [https://velog.io/@woo0_hooo/Github-github-profile-%EA%B0%84%EC%A7%80%EB%82%98%EA%B2%8C-%EA%BE%B8%EB%AF%B8%EA%B8%B0](https://velog.io/@woo0_hooo/Github-github-profile-%EA%B0%84%EC%A7%80%EB%82%98%EA%B2%8C-%EA%BE%B8%EB%AF%B8%EA%B8%B0)<br>
> capsule-render : [https://github.com/kyechan99/capsule-render](https://github.com/kyechan99/capsule-render)

<br><br><br><br>

## Daily 코딩 시간 적용하기

<br><br>

![image](https://user-images.githubusercontent.com/102353910/162474502-644e3f02-e9c2-4020-824b-60a00e7f4ef4.png)

<br><br>

하지만 굴하지 않고 다른 것을 꾸며본다.<br>그거슨 바로 프로필에 Daily 코딩 시간 표시하기!<br>내가 어느 시간대에 커밋을 가장 많이 하는지 표시하는 것이다.

<br><br>

#### 🛠️적용하기🛠️

1.  [techinpark/productive-box](https://github.com/techinpark/productive-box) `fork`
2.  github에서 새로운 `Public Gist` 생성하기
3.  새로 생성한 GIst의 URL 뒷 부분 복사해놓기
4.  토큰 생성하기 => repo와 gist 두 가지 선택한 채로 생성<br>토큰은 다시 보여주지 않으니 메모해놓기
5.  fork한 Repository의 `Settings` > `Secrets` > `Action secrets` 들어가기
6.  Secrets 등록하기 `New repository secret`

| Name     | Value                     |
| -------- | ------------------------- |
| GH_TOKEN | 생성한 github 토큰 입력   |
| GIST_ID  | gist URL 주소 뒷부분 입력 |

8.  `Action` 탭 들어가기
9.  `Enable` 눌러서 Actions 활성화 해주기
10. 프로필에서 `Pinned` 처리하기

<br>

> ### 참고⭐
>
> Github 프로필에 Daily 코딩 시간 나타내기 : [https://codesyun.tistory.com/98](https://codesyun.tistory.com/98)

<br><br>
![image](https://user-images.githubusercontent.com/102353910/162474013-d0d3ca98-9c7e-4e8c-be3a-8dc741f6e3dc.png)

<br>
적용이 잘 되었다!<br>근데 왜 나는 i'm a ealry bird / night owl 이런거 안뜨고 저렇게 뜨징..<br>저어거는 일단 하루이틀 두고 보다가 시간나면 뭐 수정해야겠따..;;<br><br>너무 초라한 내 프로필 완성😭<br>언젠간 내 프로필도 빽빽해지길 바라며... 열심히 해야겠다 !

<br><br><br><br>
