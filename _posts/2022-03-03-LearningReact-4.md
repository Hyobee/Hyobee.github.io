---
title: "4.0.0 리액트 작동원리"
permalink: /react/리액트작동원리
categories:
  - React
tags:
  - Learning React
---

## 4.1 페이지 설정
리액트를 브라우저에서 다루려면 React, ReactDOM 라이브러리를 불러와야 함.
React는 뷰를 위한 라이브러리, ReactDOM은 UI를 실제로 브라우저에 렌더링할 때 사용하는 라이브러리다.
아래 코드는 브라우저에서 리액트를 사용하기 위한 최소한의 요구사항이다.

```jsx
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Pure React Samples</title>
</head>
<body>

<!-- Target Container -->
<div id="react-container"></div>

<!-- React Library & React DOM-->
<script src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>

<script>

    // Pure React and JavaScript Code

</script>

</body>
</html>
```

## 4.2 리액트 엘리먼트
HTML을 DOM을 구사하기 위해 따라야하는 절차

### 4.2.1 전통적인 방식
전통적으로 웹사이트는 독립적인 HTML 페이지들로 만들어졌다. 사용자가 페이지 사이를 내비게이션 함에 따라 브라우저는 매번 다른 HTML문서를 요청해서 로딩할 수 있었다.

### 4.2.2 SPA(Single Page Application)
#### 유래
AJAX(Asynchronous Javascript and XML)가 생기면서 단일 페이지 애플리케이션인 SPA가 생겼다.
브라우저가 AJAX를 이용해 아주 작은 데이터를 요청해서 가져올 수 있게됨에 따라 이제는 전체 웹 애플리케이션이 한 페이지로 실행되면서 자바스크립트에 의존해 사용자 인터페이스를 갱신하게 됐다.

#### 작동원리
SPA애서 처음에 브라우저는 HTML문서를 하나 적재한다. 사용자는 사이트를 내비게이션 하지만 실제로는 같은 페이지 안에 계속 머문다. 자바스크립트는 사용자가 애플리케이션과 상호 작용하는 것에 맞춰 표시중이던 인터페이스를 없애고 새로운 사용자 인터페이스를 만든다.
사용자가 느끼기에는 한 페이지에서 다른 페이지로 이동한 것 같지만 실제로 사용자는여전히 같은 HTML페이지 안에 머물 뿐이고 자바스크립트가 모든 힘든 처리를 대신 해준다.

DOM API는 브라우저의 DOM을 변경하기 위해 자바스크립트가 사용할 수 있는 객체의 모음이다.
리액트는 브라우저 DOM을 갱신해 주기 위해 만들어진 라이브러리이다. 리액트에서는 코드로 DOM API를 직접 조작하지 않는다. 대신 리액트에게 어떤 UI를 생성할지 지시하면, 리액트가 우리 명령에 맞춰 원소 렌더링을 조절해준다.
리액트 엘리먼트는 개념상 HTML엘리먼트와 비슷하지만 실제로는 자바스크립트의 객체다.

React.createElement를 사용해 h1을 표현하는 리액트 엘리먼트를 만들 수 있다.
```jsx
React.createElement(
  "h1",             // 엘리먼트 타입
  {id: "recipe-0"}, // 엘리먼트 프로퍼티 or 태그의 속성
  "구운 연어"         // 자식노드
)

# 결과
<h1 id="recipe-0">구운연어</h1>
```

## 4.3 React DOM

### ReactDOM.render
리액트 엘리먼트를 브라우저에서 보기 위한 렌더링 메서드

```jsx
const dish = React.createElement("h1", null, "Baked Salmon")

ReactDOM.render(
  dish,                           // 렌더링할 리액트 엘리먼트
  document.getElementById('root') // 렌더링이 일어날 대상 DOM 노드
)

# 결과
<body>
  <div id="root">
    <h1>구운연어</h1>
  </div>
</body>
```
### 4.3.1 자식들 (엘리먼트 트리)
리액트는 props.children을 사용해 자식 엘리먼트들을 렌더링한다. 앞 절에서는 h1 엘리먼트의 유일한 자식으로 텍스트 엘리먼트를 렌더링 했기 떄문에 props.children이 "baked salmon"으로 설정됐다.


```jsx
<ul>
  <li>연어 900 그램</li>
  <li>신선한 로즈마리 5 가지</li>
  <li>올리브 오일 2 테이블 스푼</li>
  <li>작은 레몬 2 조각</li>
  <li>코셔 소금 1 티스푼</li>
  <li>다진 마늘 4 쪽</li>
</ul>

React.createElement(
  "ul",
  null,
  React.createElement("li", null, "연어 900 그램"),
  React.createElement("li", null, "신선한 로즈마리 5 가지"),
  React.createElement("li", null, "올리브 오일 2 테이블 스푼"),
  React.createElement("li", null, "작은 레몬 2 조각"),
  React.createElement("li", null, "코셔 소금 1 티스푼"),
  React.createElement("li", null, "다진 마늘 4 쪽")
);

const list = React.createElement(
  "ul",
  null,
  React.createElement("li", null, "연어 900 그램"),
  React.createElement("li", null, "신선한 로즈마리 5 가지"),
  React.createElement("li", null, "올리브 오일 2 테이블 스푼"),
  React.createElement("li", null, "작은 레몬 2 조각"),
  React.createElement("li", null, "코셔 소금 1 티스푼"),
  React.createElement("li", null, "다진 마늘 4 쪽")
);

console.log(list);

{
  "type": "ul",
  "props": {
    "children": [
      {"type": "li", "props": {"children": "연어 900 그램"} ...},
      {"type": "li", "props": {"children": "신선한 로즈마리 5 가지"} ...},
      {"type": "li", "props": {"children": "올리브 오일 2 테이블 스푼"} ...},
      {"type": "li", "props": {"children": "작은 레몬 2 조각"} ...},
      {"type": "li", "props": {"children": "코셔 소금 1 티스푼"} ...},
      {"type": "li", "props": {"children": "다진 마늘 4 쪽"} ...}
    ]
    ...
  }
}
```

데이터를 가지고 엘리먼트 만들기
리액트를 사용하는 경우 가장 큰 장점은 UI 엘리먼트와 데이터를 분리할 수 있다는 것이다. 리액트는 단순한 자바스크립트이기 때문에 리액트 컴포넌트 트리를 더 편하게 구성하기 위한 자바스크립트 로직을 얼마든지 추가할 수 있다.
예를 들어 배열에 재료를 저장해두고 그 배열을 리액트 엘리먼트를 map할 수 있다.
번호가 붙지 안은 리스트에 대해 다시 생각해보자. 

```jsx
React.createElement(
  "ul",
  null,
  React.createElement("li", null, "연어 900 그램"),
  React.createElement("li", null, "신선한 로즈마리 5 가지"),
  React.createElement("li", null, "올리브 오일 2 테이블 스푼"),
  React.createElement("li", null, "작은 레몬 2 조각"),
  React.createElement("li", null, "코셔 소금 1 티스푼"),
  React.createElement("li", null, "다진 마늘 4 쪽")
);

// 이 재료를 더 간단하게 표현할 수 있다.

const items = [
  "연어 900 그램",
  "신선한 로즈마리 5 가지",
  "올리브 오일 2 테이블 스푼",
  "작은 레몬 2 조각",
  "코셔 소금 1 티스푼",
  "다진 마늘 4 쪽"
];

// map을 통해 하드코딩 없이 원하는 만큼 리스트 원소를 생성할 수 있다.

React.createElement(
  "ul",
  {clsaaName: "ingredients"},
  items.map(ingredient => ReactElement("li", null, ingredient))
);

// 배열의 반복을 통해 엘리먼트 생성시 key 프로퍼티를 이용할 수 있다.

React.createElement(
  "ul",
  {clsaaName: "ingredients"},
  items.map((ingredient, i) => ReactElement("li", {key: i}, ingredient))
);

// 콘솔 경고를 없애기 위해 키를 일단은 추가하자.
```

## 4.4 리액트 컴포넌트

IngredientsList라는 이름으로 디저트를 만드는 함수를 작성해보자.

```jsx
function IngredientsList(){
  return React.createElement(
    "ul",
    {className: "ingredients"},
    React.createElement("li", null, "무염 버터 1 컵"),
    React.createElement("li", null, "크런치 땅콩 버터 1컵"),
    React.createElement("li", null, "흑설탕 1 컵"),
    React.createElement("li", null, "백설탕 1 컵"),
    React.createElement("li", null, "달걀 2 개"),
    React.createElement("li", null, "일반 밀가루 2.5 컵"),
    React.createElement("li", null, "베이킹 소다 1 티스푼"),
    React.createElement("li", null, "소금 0.5 티스푼"),
  );
}

ReactDOM.render(
  React.createElement(IngredientsList, null, null),
  document.getElementById("root")
);
```

함수가 반환하는 엘리먼트는 다음과 같다.

```jsx
<IngredientsList>
  <ul className="ingredients">
    <li>무염 버터 1 컵</li>
    <li>크런치 땅콩 버터 1컵</li>
    <li>흑설탕 1 컵</li>
    <li>백설탕 1 컵</li>
    <li>달걀 2 개</li>
    <li>일반 밀가루 2.5 컵</li>
    <li>베이킹 소다 1 티스푼</li>
    <li>소금 0.5 티스푼</li>
  </ul>
</IngredientsList>
```

위의 식은 하드코딩을 했다는 문제점이 있다.
map을 이용해 만들어보자.

```jsx
const secretIngredients = [
  "무염 버터 1 컵",
  "크런치 땅콩 버터 1컵",
  "흑설탕 1 컵",
  "백설탕 1 컵",
  "달걀 2 개",
  "일반 밀가루 2.5 컵",
  "베이킹 소다 1 티스푼",
  "소금 0.5 티스푼"
]

// IngredientsList 컴포넌트가 이 items를 map하게 해서 items 배열에 있는 모든 내용에 대해 li를 만들게 한다.

function IngredientsList(){
  return React.createElement(
    "ul",
    {className: "ingredients"},
    items.map((ingredient, i) => React.createElement("li", {key, i}, ingredient))
  );
}

// 그 후 secretIngredients를 items라는 프로퍼티로 넘기면 된다. items 프로퍼티는 createElement의 두 번쨰 인자다.

ReactDOM.render(
  React.createElement(
    IngredientsList, 
    {items: secretIngredients}, null), 
    document.getElementById("root")
  )
);
```

items라는 데이터 프로퍼티는 8가지 재료가 들어 이쓴 배열이다. 루프를 돌면서 li 태그를 만들기 때문에 푸르 인덱스를 사용해 유일한 키를 추가할 수 있다.

```jsx
<IngredientsList items="[...]">
  <ul className="ingredients">
    <li key="0">무염 버터 1 컵</li>
    <li key="1">크런치 땅콩 버터 1컵</li>
    <li key="2">흑설탕 1 컵</li>
    <li key="3">백설탕 1 컵</li>
    <li key="4">달걀 2 개</li>
    <li key="5">일반 밀가루 2.5 컵</li>
    <li key="6">베이킹 소다 1 티스푼</li>
    <li key="7">소금 0.5 티스푼</li>
  </ul>
</IngredientsList>

이런식으로 컴포넌트를 만들면 컴포넌트가 더 유연해진다. items 배열에 원소가 하나뿐이든 수백 개이든 컴포넌트는 배열의 각 원소를 리스트 원소로 렌디링할 것이다.
```

items 배열을 리액트 프로퍼티로 참조하게 변경할 수도 있다. 전역 items 에 대해 매핑을 수행하는 대신에 props 객체를 통해 items를 얻게 한다. 먼저 props를 함수에 전달하고 props.items에 대해 매핑을 수행하게 만들자.

```jsx
function IngredientsList(props){
  return React.createElement(
    "ul",
    {className: "ingredients"},
    props.items.map((igredient, i) => React.createElement("li", {key, i}, ingredient))
  );
}
```

props에서 items를 구조 분해하면 코드를 약간 더 다듬을 수 있다.

```jsx
function IngredientsList({items}){
  return React.createElement(
    "ul",
    {className: "ingredients"},
    items.map((igredient, i) => React.createElement("li", {key, i}, ingredient))
  );
}
```

IngredientsList와 관련된모든 내용은 이제 한 컴포넌트 안에 캡슐화되어 있다. 컴포넌트를 처리할 때 필요한 모든 것이 컴포넌트 내부에 들어 있다.