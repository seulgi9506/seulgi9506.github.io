---
title: "[Vanilla JS] Nomad Coders 바닐라 JS로 크롬 앱 만들기 #2"
published: true
categories:
  - Momentum
---

## On the 바닐라 JS로 크롬 앱 만들기 #2

part2에서는 JS의 완전 기초적인 내용을 가르쳐준다.<br>
강의 소개에서 초보자도 수강할 수 있는 강의라고 했던 이유인가보다.

<br><br>

## 파일 구조

![image](https://user-images.githubusercontent.com/102353910/161230388-ac7ce713-46fe-4160-8372-17f00a2f6384.png)

웹 브라우저에서는 html파일을 연다.<br>
html파일은 css와 javascript를 가져온다.<br><br>
css는 head태그 안에서 불러와준다.<br>
Javascript는 아래의 body태그 안에서 불러와준다.<br><br><br>

![image](https://user-images.githubusercontent.com/102353910/161230927-e9f1539b-ac64-40ad-8b04-4ffde4202cf0.png)

F12를 누르면 개발자탭을 볼 수 있다.<br>
Elements = html 코드<br>
오른쪽 창 = css style 코드<br>
Console = js 코드
<br><br><br>

## DataType / Variables

<br>

| DataType  | data                                            |
| --------- | ----------------------------------------------- |
| integer   | 5 / 12 / 1358 / 68948613                        |
| float     | 1.2 / 15.3669 / 543848.127768323                |
| String    | "Hello" / "How old are you?" / "256"            |
| boolean   | true / false                                    |
| null      | null                                            |
| Undefined | (there are a space but doesn't have any value.) |

<br><br>

| Variables |                                                                                                                                                     |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| const     | const로 선언한 변수는 value값이 바뀌지 않음.<br>변수를 선언할때는 항상 const로 선언하기                                                             |
| let       | let으로 선언한 변수는 바뀔 수 있음.                                                                                                                 |
| var       | var로 선언한 변수는 바뀔 수 있지만 선언부만 보고는 아래 코드에서 바뀌는지 아닌지 알 수 없음. js초기에 만들어진 변수타입.<br> 되도록 사용하지 말 것. |

<br><br>

## Arrays

    const daysOfWeek = [“mon”, “tue”, “wed”, “thu”, “fri”, “sat”]
    console.log(daysOfWeek[4])
    daysOfWeek.push(“sun”)

배열은 대괄호 안에서 선언할 수 있고, 반점으로 구분한다.<br>
배열은 0번부터 시작하며 위 배열에서 "mon"은 'daysOfWeek[0]' 에 해당한다.<br>
daysOfWeek[4] = "fri" 라는 값이 나온다.<br>
daysOfWeek.push("sun") 을 실행하면 배열의 맨 뒤에 "sun"이라는 값이 추가된다.

<br><br>

## Objects

    const  player  = {
        name:  "Seulgi",
        points:  10,
        fat:  true,
    };
    console.log(player);
    console.log(player.name);

배열이 아닌 object로 선언할 수 있다.<br>
배열은 0, 1, 2 ~ 순서로 값이 들어가기 때문에 만약<br>
const player = ["Seulgi", 10, true] 로 값을 넣어준다면<br>
"Seulgi"나 10, true 가 각각 무엇을 의미하는지 알 수 없다.<br>
object로 선언하면 각각의 value가 무엇을 의미하는지 알 수 있다.<br>

    const  player  = {
        name:  "Seulgi",
        sayHello:  function (_otherPersonsName_) {
    	    console.log("hello!"  +  _otherPersonsName_  +  " nice to meet you");
        },
    };
    console.log(player.name);
    player.sayHello(" Nino");
    player.sayHello(" Ayleen");

위의 코드처럼 object 안에 function을 넣어서 만들 수도 있다.

<br><br>

## Calculator

    const  calculator  = {
        add:  function (a, b) {
    	    console.log(a  +  b);
    	},
    	minus:  function (a, b) {
    		console.log(a  -  b);
    	},
    	divide:  function (a, b) {
    		console.log(a  /  b);
    	},
    	power:  function (a, b) {
    		console.log(a  **  b);
    	},
    };
    calculator.add(1, 2);
    calculator.minus(3, 4);
    calculator.divide(5, 6);
    calculator.power(7, 8);

중간에 니꼬쌤이 내준 계산기 만들기 숙제
<br><br>

## parseInt() : 사용자가 입력한 값을 숫자로 변환

사용자가 입력한 값을 숫자로 바꿀 수 있다.<br>
parseInt("15")<br>
괄호 안에 "15"는 쌍따옴표 안에 있어서 String타입이지만 parseInt("15") 안에 넣어주면 숫자 15로 형변환되어진다.<br>

    const  age  =  parseInt(prompt("How old r u?"));
    console.log(age);

위의 코드에서 사용자가 prompt로 입력한 숫자는 String형태로 받아지고 parseInt가 숫자 형태로 형변환 해준다.<br>
만약 사용자가 prompt에 "Hello"라는 문자를 입력하게되면 NaN(not a number)를 반환한다.<br>

<br><br>

## and(&&)와 or( || ) 연산자

    if (isNaN(age) ||  age  <  0) {
        console.log("Please write a real positive number.");
    } else  if (age  <  18) {
    	console.log("you are too young.");
    } else  if (age  >=  17  &&  age  <=  50) {
    	console.log("you can drink");
    } else  if (age  >  50  &&  age  <=  80) {
    	console.log("you should exercise");
    } else  if (age  >  80) {
    	console.log("you can do whatever you want");
    }

and와 or 연산자를 활용한 코드이다.
<br>

> **and(&&) 연산자**<br>
> true && true === true<br>
> true && false === false<br>
> false && true === false<br>
> false && false === false<br><br>

> **or // 연산자** (원래 세로 막대기 표시인데 글씨체를 설정했더니 제대로 안나와서 슬래쉬로 입력)<br>
> true // true === true<br>
> false // true === true<br>
> true // false === true<br>
> false // false === false
