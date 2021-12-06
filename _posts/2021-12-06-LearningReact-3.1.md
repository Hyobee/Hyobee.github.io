---
title:  "3.1 함수형이란 무엇인가?"
permalink: /javascript/
categories:
  - Javascript
tags:
  - Learning React
---

## 함수형의 정의
함수형 프로그래밍(종종 줄여서 FP라고 부름)은 순수 함수(pure function) 를 조합하고  
공유 상태(shared state), 변경 가능한 데이터(mutable data) 및 부작용(side-effects) 을 피하여  
소프트웨어를 만드는 프로세스이다.

1. 함수를 **변수**에 넣을 수 있다.
2. 함수를 **객체**에 넣을 수 있다.
3. 함수를 다른 **함수에 인자**로 넘길 수 있다.
4. 함수가 **함수를 반환**할 수 있다.

[객체](https://hyobee.github.io/javascript/object)

## 1. 함수를 **변수**에 넣을 수 있다.
```jsx
var log = function(message){
  console.log(message);
};

log('자바스크립트에서는 함수를 변수에 넣을 수 있습니다.');
```

```jsx
const log = message => {
  console.log(message);
};
```   

이 두 문장은 같은 일을 한다.  
두 문장 다 함수를 log라는 변수에 넣는다.  
추가로 두 번쨰 문장에서는 const를 사용했기 때문에 log를 덮어쓰지 못하게 막아준다.   
  
## 2. 함수를 **객체**에 넣을 수 있다.
```jsx
// log라는 함수에 message라는 객체를 넣었다.
// 객체 -> key:value 형태  
const obj = {
  message: "함수를 다른 값과 마찬가지로 객체에 추가할 수도 있습니다.", 
  log(message){
    console.log(message);
  };
}  

obj.log(obj.message);

// 함수를 다른 값과 마찬가지로 객체에 추가할 수도 있습니다.
// 심지어 함수를 배열에 넣을 수도 있습니다.
const messages = [
  "함수를 배열에 넣을 수도 있습니다.",
  message => console.log(message),
  "일반적인 값과 마찬가지 입니다.",
  message => console.log(message)
]

messages[1](messages[0]) // 함수를 배열에 넣을 수도 있습니다.
messages[3](messages[2]) // 함수를 배열에 넣을 수도 있습니다.
```
  
## 3. 함수를 **다른 함수에 인자**로 넘길 수 있다.
```jsx
const insideFn = logger => {
  logger("함수를 다른 함수에 인자로 넘길 수도 있습니다.");
};

insideFn(message => console.log(message));
```

## 4. 함수가 **함수를 반환**할 수 있다.

```jsx
const createScream = function(logger){
  return function(message){
    logger(message.toUpperCase() + "!!!");
  };
};

const scream = createScream(message => console.log(message));

scream("함수가 함수를 반환할 수도 있습니다.");
scream("createScream은 함수를 반환합니다.");
scream("scream은 createScream를 반환한 함수를 가르킵니다.");

// 함수가 함수를 반환할 수도 있습니다.
// createScream은 함수를 반환합니다.
// scream은 createScream를 반환한 함수를 가르킵니다.
```
함수가 함수를 인자로 받는 경우와 함수가 함수를 반환하는 경우를 고차함수라고 부른다.
createScream 고차함수를 화살표 함수로 표현할 수도 있다.

```jsx
```


관련 링크
[함수형 프로그래밍 관련 블로그글](https://sungjk.github.io/2017/07/17/fp.html)