---
title:  "3.3.1 불변성"
permalink: /javascript/3.3.1
categories:
  - Javascript
tags:
  - Learning React
---

## 불변성
함수형 프로그래밍에서는 데이터가 변할 수 없다.  
불변성 데이터는 결코 바뀌지 않는다.  
수정이 필요할 경우 원본을 복사한 사본을 수정하여 필요한 작업을 진행한다.  
  
불변성이 어떻게 작동하는지 이해하기 위해 데이터를 변경한다는 것이 어떤 의미인지를 살펴보자.

```jsx
let color_lawn = {
  title: "잔디",
  color: "#00FF00",
  rating: 0 
};
```
색상에 점수를 매기는 함수를 만들 수 있을 것이다.  
그 함수는 넘겨받은 color 객체의 rating을 변경한다.

```jsx
function rateColor(color, rating){
  color.rating= rating;
  return color;
}

console.log(rateColor(color_lawn, 5).rating); // 5
console.log(color_lawn.rating); // 5
```

자바스크립트에서 함수의 인자는 실제 데이터에 대한 참조다.  
rateColor 함수 안에서 color의 rating을 변경하면 원본 color_lawn객체의 rating도 바뀐다.  
rateColor를 다음과 같이 고쳐쓰면(color 파라미터로 전달 받은) 원본에는 아무런 해가 없이 색깔에 평점을 부여할 수 있다.

## 출처
[]()