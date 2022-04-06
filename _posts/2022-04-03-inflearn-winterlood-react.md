---
title: "[JS 기초] Inflearn 한입 크기로 잘라먹는 리액트 #1 "
published: true
categories:
  - winterlood-react
---

## 섹션0. 들어가며

간단한 강사소개와 React.js에 대한 설명을 해주셨다.<br>또 실시간으로 질문과 강의에 대한 피드백 등의 소통이 가능한 오픈카톡 채팅방 입장방법과 비밀번호도 주셨다.<br><br>이 강의에서는 Javascript 문법 기초와 Node.js에 대한 설명까지 해주고 마지막으로 간단한 프로젝트를 제작해서 실제로 배포하는 방법까지 알려준다고 한다.<br>수강 기간이 무제한이니까 언제든 듣고 싶으면 다시 들을 수 있어서 좋을 것 같다. <br>게다가 만우절 이벤트로 할인쿠폰으로 아주 저렴한 가격에 구매할 수 있었다.<br>열심히 듣겠습니다. 감사합니다!<br><br>나는 기초부분은 리마인드용으로 듣고 싶은 부분만 골라서 들었다.

<br><br>

## 2-5 조건문

if문으로 조건문을 만들 수 있다.<br>동일하게 switch 문으로도 조건문을 만들 수 있는데.<br>적절하게 break를 사용하지 않으면 아랫부분도 모두 인식되어서 전부 출력이 된다.

    let  country  =  "ko";

    if (country  ===  "ko") {
        console.log("한국");
    } else  if (country  ===  "cn") {
        console.log("중국");
    } else  if (country  ===  "jp") {
        console.log("일본");
    } else {
        console.log("미 분류");
    }

    switch (country) {
        case  "ko":
    	    console.log("한국");
    	    break;
        case  "cn":
    	    console.log("중국");
    	    break;
        case  "jp":
    	    console.log("영국");
    	    break;
        case  "uk":
    	    console.log("영국");
    	    break;
        default:
    	    console.log("미 분류");
    	    break;
    }

<br><br>

## 2-7 함수 표현식 & 화살표 함수

함수 선언 방식은 세 가지로 분류할 수 있다.

##### 1. 함수 선언식

    function  helloA() {
        return  "hello A";
    }

##### 2. 함수 표현식

    let  helloA  =  function () {
        return  "hello A";
    };

##### 3. 화살표 함수

    let  helloA  = () => {
        return  "hello A";
    };

<br>

    let  helloA  = () =>  "hello A";

<br><br>

> ### 🌟호이스팅
>
> 함수 선언식으로 만들어진 함수들은 프로그램 실행 전에 코드의 최상단으로 끌어올려진다.
> 가장 아래에 선언해도 위에서 호출해서 사용이 가능하다.
> 함수 표현식, 화살표 함수는 불가능.
>
> ex) helloB() 함수가 선언되어진 위치보다 위에서 호출되어도 상관없다.
> 하지만 helloA() 함수는 선언되어진 위치보다 위에서 호출될 수 없다.
>
> ```
> console.log(helloB());
>
> let helloA = function(){
>     return "hello A";
> }
>
> function helloB() {
>     return "hello B";
> }
> ```

<br><br>

## 2-8 콜백함수

어떤 다른 함수에 매개변수로 함수를 넘겨주는 것을 말한다.

    function  checkMood(mood, goodCallback, badCallback) {
        if (mood  ===  "good") {
    	    // 기분 좋을 때 하는 동작
    	    goodCallback();
        } else {
    	    // 기분 안좋을 때 하는 동작
    	    badCallback();
    	}
    }

    function  cry() {
        console.log("ACTION :: CRY");
    }

    function  sing() {
        console.log("ACTION :: SING");
    }

    function  dance() {
        console.log("ACTION :: DANCE");
    }

    checkMood("good", sing, cry);

<br><br>

## 2-12 배열 내장함수

### 💫forEach

배열의 첫 번째부터 마지막까지 찾을 수 있다.

    const  arr  = [1, 2, 3, 4];
    arr.forEach((elm) =>  console.log(elm));

    const  newArr  = [];
    arr.forEach(function (elm) {
        newArr.push(elm  *  2);
    });

<br><br>

### 💫map

배열의 각 요소를 모은 새 배열을 return한다.

    const  arr  =  [1,  2,  3,  4];

    const  newArr2  =  arr.map((elm)  =>  {
        return  elm  *  2;
    });

    console.log(newArr2);

<br><br>

### 💫includes

주어진 배열에서 전달 받은 인자와 일치하는 값이 존재하는지 확인(true/false)

    const  arr  =  [1,  2,  3,  4];
    let  num  =  3;
    console.log(arr.includes(num));

<br><br>

### 💫indexOf

주어진 배열에서 전달 받은 인자와 일치하는 인덱스를 반환(일치하지 않으면 -1 반환)

    const  arr  =  [1,  2,  3,  4];
    let  num  =  3;
    console.log(arr.indexOf(num));

<br><br>

### 💫findIndex

콜백함수를 전달해서 콜백함수가 true를 반환하는 첫 번째 요소의 인덱스를 반환.
일치하는 조건을 가진 요소가 두 개인 경우, 가장 먼저 만나는 요소의 인덱스를 반환.

    const  arr2  =  [
        { color:  "red"  },
        { color:  "black"  },
        { color:  "blue"  },
        { color:  "green"  }
    ];

    console.log(arr2.findIndex((elm)  =>  elm.color  ===  "red"));
    console.log(
        arr2.findIndex((elm)  =>  {
    	    return  elm.color  ===  "red";
        })
    );

    const  idx  =  arr2.findIndex((elm)  =>  {
        return  elm.color  ===  "blue";
    });

    console.log(idx);  // 인덱스 반환
    console.log(arr2[idx]);  // 요소를 반환

<br>결과
![image](https://user-images.githubusercontent.com/102353910/161417064-09182b90-4d70-4685-9d4f-9c328c0fb279.png)

<br><br>

### 💫find

조건을 만족하는 첫 번째 요소를 반환한다.

    const  arr2  =  [
    { color:  "red"  },
    { color:  "black"  },
    { color:  "blue"  },
    { color:  "green"  }
    ];

    const  element  =  arr2.find((elm)  =>  {
    return  elm.color  ===  "blue";
    });

    console.log(element);

(위에서 요소를 반환하는 코드와 같은 결과)

<br><br>

### 💫filter

콜백함수가 true를 반환하는 모든 요소를 배열로 반환

    const  arr3  = [
    { num:  1, color:  "red" },
    { num:  2, color:  "black" },
    { num:  3, color:  "blue" },
    { num:  4, color:  "green" },
    { num:  5, color:  "blue" },
    ];

    console.log(arr3.filter((elm) =>  elm.color  ===  "blue"));

<br>결과
![image](https://user-images.githubusercontent.com/102353910/161417203-8a8f3836-80c2-4c24-a3fd-9bd822e90753.png)

<br><br>

### 💫slice

begin ~ end-1 까지 반환
ex) slice(0, 2) => 0, 1 반환 / slice(0, 4) => 0, 1, 2, 3 반환

    const  arr3  =  [
    { num:  1, color:  "red"  },
    { num:  2, color:  "black"  },
    { num:  3, color:  "blue"  },
    { num:  4, color:  "green"  },
    { num:  5, color:  "blue"  }
    ];

    console.log(arr3.slice(0,  3));

<br>결과
![image](https://user-images.githubusercontent.com/102353910/161417267-6533ca27-5f55-46a6-be82-e850824862e5.png)

<br><br>

### 💫concat

명시한 배열의 뒤에 괄호안의 배열을 붙인다.

    const  arr4  = [
        { num:  1, color:  "red" },
        { num:  2, color:  "black" },
        { num:  3, color:  "blue" },
    ];

    const  arr5  = [
        { num:  4, color:  "green" },
        { num:  5, color:  "blue" },
    ];

    console.log(arr4.concat(arr5));

<br>결과
![image](https://user-images.githubusercontent.com/102353910/161417359-835461cd-6914-450d-afb2-ecc2505e126a.png)

<br><br>

### 💫sort

원본 배열을 다시 정렬(문자열 기준, 사전순)

    let  chars  =  ["나",  "다",  "가"];
    chars.sort();
    console.log(chars);

<br>결과
![image](https://user-images.githubusercontent.com/102353910/161417406-de8b28b8-1eab-4839-b810-cdbe51d519dc.png)
<br>
🌟숫자의 경우에는 sort를 전달할 비교함수를 만들어야한다.

    let  nums  =  [0,  5,  3,  30,  22,  12];

    const  compare  =  (a,  b)  =>  {
        if  (a  >  b)  {
    	    return  1;      // 클 때는 뒤로 보낸다.
        }
        if  (a  <  b)  {
    	    return  -1;     // 작을 때는 앞으로 보낸다.
        }
        return  0;          // 같을 때는 자리를 바꾸지 않는다.
    };

    nums.sort(compare);
    console.log(nums);

<br>결과
![image](https://user-images.githubusercontent.com/102353910/161418169-71b69bef-166d-40f5-839c-8710169972fb.png)

<br><br>

### 💫join

배열의 요소들을 문자열로 하나로 합쳐서 반환한다.
괄호안에 아무것도 넣지 않으면 ','를 구분자로 반환
괄호 안이 구분자가 됨.

    const  arr6  =  ["슬기",  "님",  "안녕하세요.",  "또 오셨네요."];
    console.log(arr6.join("  "));

<br>결과
![image](https://user-images.githubusercontent.com/102353910/161418222-9ddd4fe8-9cec-4865-8fcc-73f17d61f502.png)
