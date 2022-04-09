---
title: "[Vanilla JS] Nomad Coders 바닐라 JS로 크롬 앱 만들기 #6"
published: true
categories:
  - Momentum
---

## quotes

<br>

명언을 랜덤하게 보여주는 기능

<br>

```js
const  quotes  = [
	{
		quote: "I am not afraid of storms for I am learning how to sail my ship.",
		author: "Helen Keller",
	},
	{
		quote: "The greatest mistake you can make in life is to be continually fearing you will make one.",
		author: "Elbert Hubbard",
	},
	...
];

const  quote  =  document.querySelector("#quote span:first-child");
const  author  =  document.querySelector("#quote span:last-child");

const  todaysQuote  =  quotes[Math.floor(Math.random() *  quotes.length)];

quote.innerText =  todaysQuote.quote;
author.innerText =  todaysQuote.author;
```

<br>
우선 quotes라는 이름으로 명언과 이름을 담은 배열을 만들어줬다.<br>그 뒤에 명언을 랜덤하게 뽑아줄 수 있도록 Math.floor()와 Math.random()을 이용했다.
<br><br><br>

![image](https://user-images.githubusercontent.com/102353910/162557829-40f87d90-3faa-4f4a-9191-c67f89dd83ef.png)
<br>
**<mark style="background-color: #d4d4f8">Math.random()</mark>**<br> 0~1사이의 숫자를 무작위로 생성한다. 소수점을 포함한다.<br>Math.random() \* 10 => 0~9까지의 숫자를 무작위로 생성. 10은 안나온다.<br><br>하지만 우리가 필요한 값은 <br>소수점을 제외한 배열에 사용할 수 있는 자연수이다.<br>**<mark style="background-color: #d4d4f8">Math.round()</mark>**<br>소수점을 반올림한다.<br>**<mark style="background-color: #d4d4f8">Math.ceil()</mark>**<br> 소수점을 올림한다. <br>**<mark style="background-color: #d4d4f8">Math.floor()</mark>**<br>소수점을 내림한다.<br><br>따라서 랜덤함수와 소수점을 버리는 함수 두 가지를 조합해서 사용하면 <br>배열에 사용할 수 있는 랜덤한 정수를 구할 수 있다.
<br><br>
![image](https://user-images.githubusercontent.com/102353910/162558086-ae6208e0-6848-4217-a7c5-623677d304a5.png)

<br><br><br><br>

## background

<br>

배경도 마찬가지로 랜덤한 사진을 배경으로 보이게 만들어야 하기 때문에<br>명언과 똑같이 만들 수 있다.
<br>

```js
const images = ["0.jpg", "1.jpg", "2.jpg", "3.jpg", "4.jpg"];

const chosenImage = images[Math.floor(Math.random() * images.length)];

const bgImage = document.createElement("img");

bgImage.src = `img/${chosenImage}`;

document.body.appendChild(bgImage);
```

<br><br><br><br>

##### 여기까지 수행한 결과물

<br>

![image](https://user-images.githubusercontent.com/102353910/162558156-87f3c101-daab-45e9-9af1-403103068636.png)

<br><br><br><br>
