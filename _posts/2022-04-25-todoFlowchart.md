---
title: "[플로우차트] todo project 흐름도 구상 "

published: false

categories:
  - minitodo
---

📑 todo mini project flowchart.
{: .notice--primary}

<br><br><br>

## to do 리스트를 만들자 !

<br>

노트북에서 다른 것을 찾다가 실수로 'Microsoft To Do' 라는 앱을 눌렀다.<br>이런 투두 어플이 있었구나 하고 이것 저것 클릭해봤다.<br>꽤 유용한 어플이라는 생각이 들었다.<br>그런데 나같은 J성향을 가진 사람에게는 달력에 표시되는 기능이 있더라면 아주 완벽하겠다라는 생각이 들었다.<br>

<br><br>

![image](https://user-images.githubusercontent.com/102353910/165026595-7b5bb840-d104-457e-9bf0-facd3cf196e8.png)

<br>

위 화면이 `Microsoft To Do`앱이다.<br>날짜를 선택해서 기한을 추가할 수 있지만 달력으로 확인할 수 없어서 아쉬웠다.<br>

<br><br><br>

![image](https://user-images.githubusercontent.com/102353910/165026998-848fa645-198b-43af-ba84-a5bd0a0fba10.png)

<br>

날짜를 선택하면 '계획된 일정'목록에 추가된다.<br>하지만 이렇게 목록 형식으로 날짜만 보여주는 것보다 달력으로 보여준다면 사용하기에 편할 것 같다.<br>그래서 to do 리스트에 마감일과 시간도 설정할 수 있는 기능을 만들자고 생각했다.<br>그런데 그런 상세한 설정은 마치 to do 가 아닌 planner처럼 보일 수 있겠다는 생각이 들었다.<br>나는 to do 보다는 planner를 많이 사용하는 편이지만 또 일반적인 캘린더 어플은 너무 복잡해 보인다는 생각을 하고 있었다.<br>to do 처럼 사용할 수 있으면서 캘린더보다는 단순한 앱을 만들어야겠다 !

<br><br><br><br>

## 화면 구상

<br>

만들고자 하는 앱의 화면을 구상해봤다.<br>카카오 오븐을 사용했다.

<br><br>

![mini todo  main](https://user-images.githubusercontent.com/102353910/165037893-5b878748-a3f8-4d17-94e7-3dcc0dce7867.png)

![mini todo  calendar](https://user-images.githubusercontent.com/102353910/165037976-c42a6665-4e9b-47ae-a83f-3ef8572ddce7.png)

![mini todo  add](https://user-images.githubusercontent.com/102353910/165038026-810c47a6-d2a2-40ab-bd9c-3d226a737605.png)

<br><br>

기존 어플과 달리 캘린더 탭을 추가하고 캘린더에서 to do를 추가할 수도 있다.<br>화면 구상까지 마쳤으니 이제 진짜 있어야할 기능과 있으면 좋을 것 같은 기능을 나눠서 정리해보겠다.

<br><br>

> #### 📌 만들 기능
>
> - 할 일 목록 / 할 일 추가 / 할 일 개수 표시
> - 완료된 할 일 표시
> - 중요 표시 / 표시 후 중요 목록으로 추가
> - 새로운 목록 생성
> - 캘린더 표시 / 캘린더에서 할 일 추가 가능

<br>

> #### ➿ 꼭 필요하진 않지만 있으면 좋을 것 같은 기능
>
> - 배경 색을 원하는대로 설정할 수 있는 기능
