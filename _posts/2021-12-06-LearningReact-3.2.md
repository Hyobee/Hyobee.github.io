---
title:  "3.2 명령형 프로그래밍과 선언적 프로그래밍 비교"
permalink: /javascript/
categories:
  - Javascript
tags:
  - Learning React
---

## 선언적 프로그래밍
선언적 프로그래밍은 필요한 것을 달성하는 과정을 하나하나 기술하는 것보다  
필요한 것이 어떤 것인지를 기술하는 것에 더 방점을 두고  
애플리케이션의 구조를 세워나가는 프로그래밍 스타일이다.

## 명령형 프로그래밍
코드로 원하는 결과를 달성해 나가는과정에만 관심을 두는 프로그래밍 스타일이다.

선언적 프로그래밍 방식이 더 읽기 쉽고, 그렇기 때문에 더 추론하기 쉽다.

```jsx
const {Render} = ReactDOM;

const Welcome = () => {
  <div id="welcome">
    <h1>Hello World</h1>
  </div>
};

render(
  <Welcome />,
  document.getElementById('target');
);
```

리액트는 선언적이다. 여기서 Welcome컴포넌트는 렌더링할 DOM에 대해 기술한다.
render 함수는 컴표넌트에 있는 시기에 따라 DOM을 만든다.
이과정에서 실제 DOM이 어떻게 만들어져야 하는지에 대한 내용은 추상화를 통해 사라진다.
이 코드를 보면 Welcome 컴포넌트를 target이라는 id를 가지는 엘리먼트 안에 렌더링 하고 싶어 한다는 프로그래머의 의도가 더 명확히 드러난다.

## 출처
[]()