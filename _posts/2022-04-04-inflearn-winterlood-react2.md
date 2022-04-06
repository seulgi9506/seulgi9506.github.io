---
title: "[JS 응용] Inflearn 한입 크기로 잘라먹는 리액트 #2 "
published: true
categories:
  - winterlood-react
---

## 3-1 Truthy & Falsy

Truthy 와 Falsy는 변수에 할당된 값을 True나 False로 판단하는 것을 말한다.<br> 이 Truthy와 Falsy의 속성을 논리 연산에 활용할 수 있다.<br><br>
**Truthy와 Falsy에 해당하는 값**

> **True가 아니어도 True로 평가하는 Truthy**
>
> - "문자열"
> - [] (빈 배열)
> - { } (빈 객체)
> - function() { } (빈 함수)
>
> **False가 아니어도 False로 평가하는 Falsy**
>
> - " " (빈 문자열)
> - 0
> - null
> - undefined
> - NaN

<br>
<iframe src="https://codesandbox.io/embed/gifted-booth-ib3idy?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="gifted-booth-ib3idy"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<br><br>

## 3-2 삼항 연산자

> 조건식 **?** True 일 때 **:** False 일 때

삼항 연산자를 사용하여 조건문을 한 줄로 줄일 수 있다.

    let  a  =  3;

    if (a  >=  0) {
        console.log("양수");
    } else {
        console.log("음수");
    }

위와 같은 조건문을 삼항 연산자로 바꾸면 아래처럼 쓸 수 있다.

    a  >=  0  ?  console.log("양수") :  console.log("음수");

<br><br>

## 3-3 단락 회로 평가

왼쪽에서 오른쪽으로 연산하는 논리연산자의 연산 순서를 이용하는 문법이다.

    false && true

and 연산의 경우 앞 부분이 false이기 때문에 앞만보고 false로 판단할 수 있다.<br>

    true || false

or 연산의 경우 앞의 true만 봐도 전체가 true임을 할 수 있기때문에 연산이 종료된다.

<br><br>

## 3-4 조건문 업그레이드

내장함수인 includes를 이용해 조건문을 더 쉽게 사용할 수 있다.

    function  isKoreanFood(food) {
        if (food === "불고기" || food === "비빔밥" || food === "떡볶이") {
    	    return  true;
        }
        return  false;
    }

위와 같은 조건문을 includes를 이용하여 아래처럼 사용할 수 있다.

    function  isKoreanFood(food) {
        if (["불고기", "떡볶이", "비빔밥"].includes(food)) {
    	    return  true;
        }
        return  false;
    }

<br><br>

## 3-5 비 구조화 할당

다른 말로 '구조 분해 할당' 이라고도 한다.<br>아래와 같이 배열에 담겨있는 값을 각각의 변주에 담아주고 싶을 때,<br>아래처럼 1번이나 2번의 방법으로 담아줄 수 있을 것이다.<br>하지만 비 구조화 할당 방법을 사용하면 3번처럼 값을 담아줄 수 있다.

    let arr = ["one", "two", "three"];

    (1)
    let one = arr[0];
    let two = arr[1];
    let three = arr[2];

    (2)
    let [one, two, three] = arr;

    (3)
    let [one, two, three] = ["one", "two", "three"];

<br>객체도 비 구조화 할당이 가능하다.

    let  object  = { one:  "one", two:  "two", three:  "three" };
    let { one, two, three } =  object;

<br><br>

## 3-6 spread 연산자

spread 연산자는 객체의 중복되는 요소들을 계속 반복하는 것을 막아준다.

<iframe src="https://codesandbox.io/embed/intelligent-satoshi-urnpfs?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="intelligent-satoshi-urnpfs"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
   ></iframe>

<br>
배열에서도 사용이 가능하다.<br>
<iframe src="https://codesandbox.io/embed/muddy-http-fm7sru?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="muddy-http-fm7sru"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<br>spread 연산자를 사용하면 중간에 다른 값을 추가하기도 더 쉬워진다.
<br><br>

## 3-7 동기 & 비동기

#### < 동기방식의 처리 ><br>

Thread(일꾼)가 코드가 작성된 순서대로 작업을 처리한다.<br> 이 전 작업이 진행 중일 때는 다음 작업을 수행하지 않고 기다린다.<br>만약 웹사이트에서 버튼 하나하나마다 30초씩 긴 시간이 걸린다면 하나의 작업이 종료되기 전 까지 올 스탑이 되기 때문에 전반적인 흐름이 느려지는 성능상의 문제가 발생하게 된다.<br><br>MultiThread방식으로 작동시키면 작업을 분할 할 수 있지만 <br> Javascript는 SingleThread로 동작한다.(일꾼을 늘릴 수 없음)<br>이런 상황에서는 Thread가 하나일지라도 여러개의 작업을 동시에 실행시키면 된다. <br> => 비동기처리방식 <br> => 하나의 작업이 Thread를 점유하지 않는 방식(논 블로킹 방식)<br>콜백함수를 붙여서 비동기 처리의 결과를 확인할 수 있다.

    // 동기적 방식

    function  taskA() {
        console.log("A작업 끝");
    }

    taskA();
    console.log("코드 끝");

taskA가 종료되기 전 까지 "코드 끝"은 실행되지 않음.

    // 비동기 방식

    function  taskB(a, b, cb) {
        setTimeout(() => {
    	    const  res  =  a  +  b;
    	    cb(res);
        }, 3000);
    }

    function  taskC(a, cb) {
        setTimeout(() => {
    	    const  res  =  a  *  2;
    	    cb(res);
        }, 1000);
    }

    function  taskD(a, cb) {
        setTimeout(() => {
    	    const  res  =  a  *  -1;
    	    cb(res);
        }, 2000);
    }

    taskB(4, 5, (b_res) => {
        console.log("b result : ", b_res);
        taskC(b_res, (c_res) => {
    	    console.log("c result : ", c_res);
    	    taskD(c_res, (d_res) => {
    		    console.log("D result : ", d_res);
    	    });
        });
    });

비동기 방식을 사용하면 위처럼 복잡해 보이는 구조로 실행이 되는데 이를 '콜백 지옥'이라고 부른다.<br>Promise 객체를 사용하여 콜백지옥을 탈출할 수 있다.
<br><br>

## 3-8 Promise : 콜백 지옥 탈출

자바스크립트의 비동기를 돕는 객체이다.<br>더 이상 비동기처리 함수에 콜백을 줄지어 전달하지 않아도 된다.<br><br>

<div class="mermaid"> 
graph LR
A(pending) -->|resolve| B(fulfilled)
A(pending) -->|reject| C(rejected)
</div>

<br>
비동기 작업이 가질 수 있는 3가지 상태이다.<br>(비동기 작업은 한 번 성공하거나 실패하면 그대로 작업이 끝난다.)<br><br>
- pending(대기 상태) : 현재 비동기 상태로 작업이 진행 중이거나 작업을 시작할 수 없는 문제 상태
- fulfilled(성공) : 비동기 작업이 의도한대로 정상적으로 완료된 상태
- rejected(실패) : 비동기 작업이 모종의 이유로 실패한 상태
<br><br>
콜백함수의 인자로 resolve와 reject가 사용된다.<br><br><br>

> 예시)<br>

<iframe src="https://codesandbox.io/embed/agitated-roman-rdl7gx?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="agitated-roman-rdl7gx"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

> 비동기 작업 자체(Promise)를 저장할 상수(asyncTask)를 만들어 준 다음에<br>new라는 키워드로
> Promise객체를 생성하면서 <br> Promise객체의 생성자로 비동기작업의 실질적인 실행함수 executor를 넘겨주게
> 되면<br>자동으로 executor 함수가 실행된다.

위에서 만들었던 taskB, taskC, taskD 역시 Promise 객체로 콜백지옥을 탈출시켜줄 수 있다.

<iframe src="https://codesandbox.io/embed/gracious-paper-sy6q9d?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="gracious-paper-sy6q9d"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

".then"으로 코드를 연속으로 실행해주는 것을 "**then chaining**"이라고 한다.<br>then chaining을 사용했을 때 장점은 아래처럼 중간에 다른 코드를 수행할 수도 있다는 것이다.<br>

    const  bPromiseResult  =  taskB(5, 1).then((b_res) => {
        console.log("B result : ", b_res);
        return  taskC(b_res);
    });

    console.log("asdfasdfad");
    console.log("asdfasdfad");
    console.log("asdfasdfad");
    console.log("asdfasdfad");

    bPromiseResult
        .then((c_res) => {
    	    console.log("C result : ", c_res);
    	    return  taskD(c_res);
        })
        .then((d_res) => {
    	    console.log("D result : ", d_res);
    });

<br><br>

## 3-9 async & await

#### async

async를 함수에 붙여주면 자동적으로 Promise를 리턴하는 비동기 함수가 되기 때문에 Promise를 더 가독성 있게 작성할 수 있다.

<iframe src="https://codesandbox.io/embed/cool-pond-lxilb7?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="cool-pond-lxilb7"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<br><br>

#### await

await은 async 함수 안에서만 동작한다.<br>await은 Promise가 처리될 때 까지 기다린다.<br>결과는 그 이후에 반환된다.

<iframe src="https://codesandbox.io/embed/elated-hermann-lfxerh?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="elated-hermann-lfxerh"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<br><br>

## 3-10 API 호출하기

#### API(Application Programming Interface) 응용 프로그램 프로그래밍 인터페이스

<br>
응용프로그램에서 사용할 수 있도록, 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻한다.<br>주로 파일 제어, 창 제어, 화상 처리, 문자 제어 등을 위한 인터페이스를 제공한다.<br><br>
개발자들을 위해 무료로 API에 대해서 더미데이터를 응답해주는 open API서비스인 [JSON placeholder](https://jsonplaceholder.typicode.com/)를 이용해 API를 사용해보았다.<br><br>

<iframe src="https://codesandbox.io/embed/busy-surf-0mpdlw?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="busy-surf-0mpdlw"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
