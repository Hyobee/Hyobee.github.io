---
title:  "3.3.2 순수 함수"
permalink: /javascript/
categories:
  - Javascript
tags:
  - Learning React
---

## 순수 함수
파라미터(매개변수, 인자)에 의해서만 반환값이 결정되는 함수를 뜻한다.  
  
순수 함수는 최소한 하나 이상의 인수를 받고 인자가 같으면 항상 같은 값이나 함수를 반환한다.
순수 함수에는 부수 효과가 없다.  
부수효과란 전역 변수를 설정하거나, 함수내부나 애플리케이션에 있는 다른 상태를 변경하는 것을 말한다.  
순수 함수는 인수를 변경 불가능한 데이터로 취급한다.  
순수 함수를 이해하기 위해 순수하지 않은 함수를 먼저 하나 살펴보자.

```jsx
const frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
};

function selfEducation(){
  frederick.canRead = true;
  frederick.canWrite = true;
  return frederick;
}

selfEducation();
console.log(frederick);

// {name: "Frederick Douglass", canRead: true, canWrite: true}
```
selfEducation함수는 순수하지 않다. 그 함수는 인자를 취하지 않으며, 값을 반환하거나 함수를 반환하지도 않는다.
또한 자신의 영역 밖에 있는 frederick이라는 변수를 바꾸기까지 한다.
selfEducation 함수가 호출되면 '세계'의 일부분이 바뀐다. 즉 함수 호출에 따른 부수 효과가 발생한다.

이제 selfEducation가 파라미터(인자, 매개변수)를 받게 만들자.
```jsx
const frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
};

const selfEducation = (person) => {
  person.canRead = true;
  person.canWrite = true;
  return person;
};

console.log(selfEducation(frederick));
console.log(frederick);

// {name: "Frederick Douglass", canRead: true, canWrite: true}
// {name: "Frederick Douglass", canRead: true, canWrite: true}
```

파라미터를 받긴 하지만, 이 selfEducation 함수도 순수하지 않다.  
이 함수에도 부수효과가 있기 때문이다.
이 함수를 호출하면 인수로 넘긴 객체의 필드가 바뀐다. 
이 함수에 전달 된 객체를 불변 데이터로 취급한다면 순수 함수를 얻을 수 있을 것이다.
받은 파라미터를 변경하지 않도록 함수 본문을 다시 작성하자.

```jsx
const frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
};

const selfEducation = (person) => {
  ...person,
  canRead = true,
  canWrite = true
};

console.log(selfEducation(frederick));
console.log(frederick);

// {name: "Frederick Douglass", canRead: true, canWrite: true}
// {name: "Frederick Douglass", canRead: false, canWrite: false}
```

## 결론
순수 함수는 함수 프로그래밍의 또 다른 핵심 개념이다.  
순수 함수를 이용하면 애플리케이션의 상태에 영향을 미치지 않기 떄문에 코딩이 편해진다.  
함수를 사용할 때 다음 세 가지 규칙을 따르면 순수 함수를 만들수 있다.

> 1. 순수 함수는 파라미터를 최소 하나 이상을 받아야한다.
> 2. 순수 함수는 값이나 다른 함수를 반환해야 한다.
> 3. 순수 함수는 인자나 함수 밖에 있는 다른 변수를 변경하거나, 입출력을 수행해서는 안된다.


### 인자 = 매개변수 = 파라미터

```jsx
function 함수(aaa, bbb){
    return aaa+bbb;
}
//여기에서 aaa,bbb가 파라미터라고 할 수 있다.
//함수의 정의에서 사용되는 변수를 파라미터라고 한다.
```

### 인수 = 아규먼트
```jsx
함수(3,4);
/**
여기에서 3,4 의 값이 인수(Argument)이다. 아규먼트
파라미터의 값으로 아규먼트 3과 4를 대입하였다. 라는 의미가 성립
**/
```

```jsx
```

## 출처
[인수(Argument)와 인자(Parameter, 매개변수)의 차이](https://amagrammer91.tistory.com/9)