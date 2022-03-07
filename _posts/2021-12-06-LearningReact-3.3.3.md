---
title: "3.3.3 데이터 변환"
permalink: /javascript/3.3.3
categories:
  - Javascript
tags:
  - Learning React
---

## 데이터 변환
Array.map  
Array.reduce  
Array.join

```jsx
const schools = ["Yorktown", "Washington & Lee", "Wakefield"];
```

## Array.join
Array.join 함수를 사용하면 콤마(,)로 각 학교를 구분한 문자열을 얻을 수 있다.

```jsx
const schools = ["Yorktown", "Washington & Lee", "Wakefield"];

console.log(school.join(","));
// "Yorktown, Washington & Lee, Wakefield"
```

## Array.filter
Array.filter는 술어를 (즉 불린 값, true나 false를 변수를 반환하는 함수) 유일한 인자로 받는다.
배열에서 원소를 제거해야 할 필요가 있다면 Array.pop이나 Array.splice 보다는 Array.filter를 사용하자.
Array.filter는 순수 함수다.

"W"로 시작하는 학교만 들어 있는 새로운 배열 만들기
```jsx
const schools = ["Yorktown", "Washington & Lee", "Wakefield"];
const wSchools = schools.filter(school => school[0] === "W");
```


```jsx
```

## 출처
[]()