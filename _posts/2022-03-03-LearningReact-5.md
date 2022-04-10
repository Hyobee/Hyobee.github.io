---
title: "5.0.0 JSX를 사용하는 리액트"
permalink: /react/JSX
categories:
  - React
tags:
  - Learning React
---

## 5.1 JSX로 리액트 엘리먼트 정의하기
컴포넌트 프로퍼티는 문자열과 자바스트립트 식의 2가지 유형이 있다.  
자바스크립트 식에는 배열, 객체, 함수 등이 포함된다.  
**배열, 객체, 함수 등의 자바스크립트 값을 포함시키려면 자바스크립트값 주변을 중괄호로 감싸야만 한다.**  
>* 자바스크립트식 = 중괄호로 감싼 코드

## 5.1.1 JSX 팁

### 내포된 컴포넌트
JSX 에서는 다른 컴포넌트의 자식으로 컴포넌트를 추가할 수 있다. 예를 들에 IngredientsList 안에 Ingredient를 여러번 추가할 수 있다.

```jsx
<IngredientsList>
  <Ingredient/>
  <Ingredient/>
  <Ingredient/>
</IngredientsList>
```

### className
자바스크립트에서 class가 예약어이므로 class 속성 대신 className을 사용한다.
```jsx
<h1 className="fancy">구운연어</h1>
```

### 자바스크립트식
중괄호로 자바스크립트 식을 감싸면 중괄호 안의 식을 평가해서 결과값을 사용해야한다는 뜻이다.  
예를 들어 엘리먼트 안에 title프로퍼트 값을 출력하고 싶다면 자바스크립트 식을 사용해 값을 집에 넣을 수 있다. 변수를 평가한 값이 엘리먼트 안에 들어간다.

```jsx
<h1>{title}</h1>
```

문자열이 아닌 다른 타입의 값도 자바스트립트 식 안에 넣아야 한다.

### 평가
중괄호 안에 들어간 자바스크립트 코드는 그 값을 평가받는다.  
이는 덧셈이나 문자열 이어붙임 등의 여러 연산이 일어날 수 있다는 뜻이다. 또 자바스크립트 식 안에 함수 호출 구문이 있다면 그 함수가 호출된다는 뜻이기도 하다.

```jsx
<h1>{"Hello" + title}</h1>
<h1>{title.toLowerCase().replace}<ß/h1>
```

## 5.1.2 배열을 JSX로 매핑하기
JSX는 자바스크립트이므로 자바스크립트 함수 안에서 JSX를 직접 사용할 수 있다. 예를 들어 배열을 JSX 엘리먼트로 변환할 수 있다.

```jsx
<ul>
  {props.ingredients.map((ingredient, i) => (<li key={i}>{ingredient}</li>))}
  <li></li>
</ul>
```

JSX는 깔끔하고 읽기 쉽지만, **브라우저는 JSX를 해석할 수 없다.** createElement나 팩토리를 사용해 모든 JSX를 변환해야 한다. 다행히 이런 작업에 쓸 수 있는 바벨이라는 유용한 도구가 있다.

## 5.2 바벨(컴파일)
대부분의 소프트웨어 언어는 소스 코드를 컴파일한다.  
자바스크립트는 *1)인터프리터 언어라*서 브라우저가 코드 텍스트를 해석하기 때문에 *2)컴파일*할 필요가 없다.   
  
하지만 모든 브라우저가 최신 자바스크립트 문법을 지원하지는 않는다.   
그리고 어떤 브라우저도 JSX를 지원하지 않는다. 우리는 JSX와 함께 최신 자바스크립트 기능을 활용하고 싶기 때문에 **우리가 작성한 코드를 해석할 수 있는 코드로 변환해줄 수단**이 필요하다.  
이런 변환과정을 컴파일링이라고 부르며 바벨이 그런일을 한다.

### 1)인터프리터 언어
컴파일러를 거쳐서 기계어로 변환되지 않고 바로 실행되는 프로그래밍 언어.  
목적 파일이 없기 때문에 빌드시간이 없고, 코드가 작성될 때마다 인터프리터가 한 줄씩 해석해서 바로 명령어를 실행
문법적인 오류가 있어도 실행은 시작된다.

### 1)컴파일 언어
반드시 기계어로 컴파일되어야만 실행시킬 수 있는 프로그래밍 언어
코드를 기계어로 번역해 (컴파일) 목적 파일을 만드는 시간이 필요하다. 
컴파일할 때 오류가 있다면, 기계어 번역을 통해 빌드되지 않아 실행도 되지 않는다.

### 2)컴파일
소스 코드 파일을 실행 파일, 라이브러리 등의 Object 파일로 바꾸는 작업 


## 5.3 JSX로 작성한 조리법
JSX는 코드에서 리액트 엘리먼트를 멋지고 깔끔하게 기술할 수 있게 해주며 JSX로 작성한 코드는 작성자 스스로 볼 때도 이해하기 쉽고   
리액트 커뮤니티의 다른 엔지니어들이 볼 때도 거의 즉시 이해할 수 있을 정도로 읽기 좋다.  
단점은 브라우저가 해석하지 못하기 때문에 JSX를 수수한 리액트로 변환해 주어야 한다.

```jsx
const data = [
  {
    "name": "Baked Salmon",
    "ingredients": [
      {"name": "연어", "amount": "500", "measurement": "그램"},
      {"name": "잣", "amount": "1", "measurement": "컵"},
      {"name": "버터상추", "amount": "2", "measurement": "컵"},
      {"name": "옐로 스쿼시(Yellow Squash, 호박의 한 종류)", "amount": "1", "measurement": "개"},
      {"name": "올리브 오일", "amount": "0.5", "measurement": "컵"},
      {"name": "마늘", "amount": "3", "measurement": "쪽"}
    ],
    "steps": [
      "오븐을 180도로 예열한다.",
      "유리 베이킹 그릇에 올리브 오일을 두른다.",
      "연어, 마늘, 잣을 그릇에 담는다.",
      "오븐에서 15분간 익힌다.",
      "옐로 스쿼시를 추가하고 다시 30분간 오븐에서 익한다.",
      "오븐에서 그릇을 꺼내서 15분간 식힌 다음에 상추를 곁들여서 내놓는다."
    ]
  },
  {
    "name": "생선 타코",
    "ingredients": [
      {"name": "흰살생선", "amount": "500", "measurement": "그램"},
      {"name": "치즈", "amount": "1", "measurement": "컵"},
      {"name": "아이스버그 상추", "amount": "2", "measurement": "컵"},
      {"name": "토마토", "amount": "2", "measurement": "개"},
      {"name": "또띠아", "amount": "3", "measurement": "개"},
    ],
    "steps": [
      "생선을 그릴에 익힌다.",
      "또띠아 3장 위에 생선을 얹는다.",
      "또띠아에 얹은 생선위에 상추, 토마토, 치즈를 얹는다."
    ]
  }
]
```

위의 데이터는 자바스크립트 객체가 2개 포함된 배열이다.   
각 객체에는 조리법의 이름, 필요한 재료 리스트, 그리고 조리 절차가 들어있다. 
이런 조리법을 가지고 2가지 컴포넌트가 들어있는 UI를 만들 수있다.  
  
Menu 컴포넌트는 조리법의 목록을 표시하고  
Recipe 컴포넌트는 각 조리법의 UI를 표현한다.  
DOM에 렌더링해야하는 대상은 Menu 컴포넌트이다. 데이터를 Menu컴포넌트의 recipes 프로퍼티로 넘긴다.

```jsx
// 데이터는 조리법 객체의 배열이다.
var date = [...];

// 조리법 하나를 표현하는 상태가없는 함수 컴포넌트다.
const Recipe = (props) => ( ... );

// 조리법으로 이뤄진 메뉴를 표현하는 상태가 없는 함수 컴포넌트다.
const Menu = (props) => ( ... );

// ReactDOM.render를 호출해서 Menu를 현재의 DOM 안에 렌더링한다.
ReactDOM.render(
  <Menu recipes="{data}" title="맛있는 조리법" />,
  document.getElementById("root")
);
```

### Menu component
```jsx
function Menu(props){
  return(
    <article>
      <header>
        <h1>{props.title}</h1>
        <div className="recipes">
        .
        .
        .
        </div>
      </header>
    </article>
  )
}
```

### Menu 내 recipe component
```jsx
<div className="recipes">
  {props.recipe.map((recipe, i) => (
    <Recipe
      key={i}
      name={recipe.name}
      ingredients={recipe.ingredients}
      step={recipe.steps}
    />
  ))}
</div>
```

### Menu 내 recipe component 개선
```jsx
{
  props.recipe.map((recipe, i) => <Recipe key={i} {...recipe} />);
}
```

**스프레드 연산자**는 recipe 객체의 각 필드를 Recipe 컴포넌트의 프로퍼티로 추가해준다. 
이런 단축 표기법은 모든 프로퍼티를 Recipe 컴포넌트에게 제공한다.
이런 기능이 좋을 때도 있지만 컴포넌트에 너무 많은 프로퍼티를 추가하게 될 수도 있다.

### Menu component 개선
Menu component를 개선시킬 수 있는 다른 부분으로는 props인자를 받는 부분이 있다. 객체 구조분해를 사용하면 이 함수 내부로 변수 영역을 한정시킬 수 있다. 이렇게 하면 직접 title과 recipe를 사용할 수 있고 항상 props를 덧붙여야하는 번거로움을 줄일 수 있다.

```jsx
function Menu({props, recipes}){
  return(
    <article>
      <header>
        <h1>{props.title}</h1>
        <div className="recipes">
          {recipes.map((recipe, i) => 
            <Recipe key={i} {...recipe} />
          )}
        </div>
      </header>
    </article>
  )
}
```

이제 각 조리법을 처리하는 코드를 작성하자.

```jsx
function Recipe({name, ingredients, steps}){
  return(
    <section id={name.toLowerCase().replace(/ /g, "-")}>
      <h1>{name}</h1>
      <ul className="ingredients">
        {ingredients.map((ingredient, i) => (
          <li key={i}>{ingredient.name}</li>
        ))}
      </ul>
      <section>
        <h2>조리 절차</h2>
        {step.map((step, i) => (
          <p key={i}>{step}</p>
        ))}
      </section>
    </section>
  )
}
```

이 컴포넌트도 상태가 없는 함수 컴포넌트이다. 각 조리법에는 이름에 해당하는 문자열, 재료를 표현하는 객체의 배열, 조리 절차를 표현하는 문자열이 들어있다. 객체 구조 분해를 사용하면 각 필드를 로컬 영역 안에서 변수로 뽑아낼 수 있다. 따라서 props.name, props.ingredient, props.steps 처럼 귀찮게 props를 앞에 붙이지 않고도 각 필드를 쉽게 사용할 수 있다.

Recipe 컴포넌트 안에 있는 첫 번째 자바스크립트 식은 루트 section의 id속성을 설정하는 식이다. 이 식은 조리법의 이름을 소문자로만 이뤄진 문자열로 바꾸고, 공백()을 대시(-)로 바꿔서 UI의 id속성으로 사용한다. 한글은 큰 영향이 없지만 영어라면 "Baked Salmon"이 "baked-salmon"으로 바뀐다. 그 외에 h1 자식 텍스트 노드로 name의 값이 사용된다.

ul 내부에 있는 자바스크립트 식은 map 을 사용해 각 재료를 li 엘리먼트로 변환한다. 조리법을 표시하는 section 안에서도 비슷하게 map을 사용해 각 조리 단계를 p 엘리먼트로 변환해 표시한다.

```jsx
const data = [
  {
    "name": "Baked Salmon",
    "ingredients": [
      {"name": "연어", "amount": "500", "measurement": "그램"},
      {"name": "잣", "amount": "1", "measurement": "컵"},
      {"name": "버터상추", "amount": "2", "measurement": "컵"},
      {"name": "옐로 스쿼시(Yellow Squash, 호박의 한 종류)", "amount": "1", "measurement": "개"},
      {"name": "올리브 오일", "amount": "0.5", "measurement": "컵"},
      {"name": "마늘", "amount": "3", "measurement": "쪽"}
    ],
    "steps": [
      "오븐을 180도로 예열한다.",
      "유리 베이킹 그릇에 올리브 오일을 두른다.",
      "연어, 마늘, 잣을 그릇에 담는다.",
      "오븐에서 15분간 익힌다.",
      "옐로 스쿼시를 추가하고 다시 30분간 오븐에서 익한다.",
      "오븐에서 그릇을 꺼내서 15분간 식힌 다음에 상추를 곁들여서 내놓는다."
    ]
  },
  {
    "name": "생선 타코",
    "ingredients": [
      {"name": "흰살생선", "amount": "500", "measurement": "그램"},
      {"name": "치즈", "amount": "1", "measurement": "컵"},
      {"name": "아이스버그 상추", "amount": "2", "measurement": "컵"},
      {"name": "토마토", "amount": "2", "measurement": "개"},
      {"name": "또띠아", "amount": "3", "measurement": "개"},
    ],
    "steps": [
      "생선을 그릴에 익힌다.",
      "또띠아 3장 위에 생선을 얹는다.",
      "또띠아에 얹은 생선위에 상추, 토마토, 치즈를 얹는다."
    ]
  }
]

function Recipe({name, ingredients, steps}){
  return(
    <section id={name.toLowerCase().replace(/ /g, "-")}>
      <h1>{name}</h1>
      <ul className="ingredients">
        {ingredients.map((ingredient, i) => (
          <li key={i}>{ingredient.name}</li>
        ))}
      </ul>
      <section>
        <h2>조리 절차</h2>
        {step.map((step, i) => (
          <p key={i}>{step}</p>
        ))}
      </section>
    </section>
  )
}

function Menu({props, recipes}){
  return(
    <article>
      <header>
        <h1>{props.title}</h1>
        <div className="recipes">
          {recipes.map((recipe, i) => 
            <Recipe key={i} {...recipe} />
          )}
        </div>
      </header>
    </article>
  )
}

ReactDOM.render(
  <Menu recipes="{data}" title="맛있는 조리법" />,
  document.getElementById("root")
);
```

## 5.4 리액트 프래그먼트

```jsx
function Cat({name}){
  return <h1>고양이 이름은 {name} 입니다.</h1>
}
ReactDOM.render(<Cat name="나비" />, document.getElementById("root"));
```
태그를 React.Fragment로 감싸주자.

```jsx
function Cat({name}){
  return(
    <React.Fragment>
      <h1>고양이 이름은 {name} 입니다.</h1>
      <p>이 고양이는 멋져요.</p>
    </React.Fragment>
  )
}

# 축약형
function Cat({name}){
  return(
    <>
      <h1>고양이 이름은 {name} 입니다.</h1>
      <p>이 고양이는 멋져요.</p>
    </>
  )
}
```

## 5.5 웹팩 소개
웹팩은 모듈 번들러로 알려져있다. 모듈 번들러는 다른 파일들(Javascript, CSS, JSX, ESNext 등)을 받아서 한 파일로 묶어준다. 모듈을 하나로 묶어서 얻는 2가지 이익은 모듈성과 네트워크 성능이다.
모듈성은 여러분의 소스 코드를 작업하기 쉽게 여러 부분 또는 모듈로 나눠서 다룰 수 있게 해준다. 특히 팀 환경에서 모듈성이 중요하다.

의존관계에 있는 여러 파일들을 묶은 번들을 브라우저가 한 번만 읽기 때문에 네트워크 성능이 좋아진다. 각 script 태그는 HTTP요청을 만들어낸다. 그런 HTTP요청마다 약간의 시간지연이 발생한다. 모든 의존관계를 한 파일에 넣으면 모든 파일을 단 한번의 HTTP요청으로 가져올 수 있으므로 추가 시간지연을 방지할 수 있다.

### 컴파일 외에 웹팩이 처리할 수 있는 일은 다음과 같다.
```jsx
- 코드분리
코드를 여러 덩어리로 나눠서 필요할 때 각각 로딩할 수 있다. 
때로 이를 롤업이나 레이어라고 부른다. 
코드를 분리는 여러 다른 페이지나 디바이스에서 필요한 자원을 따로 나눠서 더 효율적으로 처리하기 위함이다.

- 코드축소
공백, 줄바꿈, 긴 변수 이름, 불필요한 코드 등을 없애서 파일의 크기를 줄여준다.

- 특징 켜고 끄기
코드의 기능을 테스트 해야 하는 경우 코드를 각각의 환경에 맞춰 보내준다.

- HMR
소스 코드가 바뀌는지 감싲해서 변경된 모듈만 즉시 갱신해준다.
```

### 웹팩 모듈 번들러의 장점

```jsx
- 모듈성
모듈패턴을 사용해 모듈을 외부에 익스포트하고 나중에 그 모듈을 필요한 곳에 임포트해서 쓸 수 있으면 
애플리케이션 소스 코드를 더 관리하기 쉬운 규모로 나눌 수 있다. 
각 팀이 서로 다른 파일에 작업을 진행하고 프로덕션으로 보내기 전에 전체를 한 파일로 묶으면서 
정적으로 오류를 검사할 수 있으므로 여러팀이 쉽게 협업할 수 있다.

- 조합
모듈을 사용하면 애플리케이션을 효율적으로 구축할 수 있는 작고 단순하며 재사용이 쉬운 리액트 컴포넌트를 구축할 수 있다. 
컴포넌트가 작고 단순하다면 애플리케이션을 향상시키기 위해 그 컴포넌트 전체를 완전히 변경하기도 더 쉽다.

- 속도
모든 애플리케이션 모듈과 의존 관계를 하나의 클라이언트 번들로 묶으면 
여러 파일을 HTTP로 요청함에 따라 발생할 수 있는 시간지연이 없어져서 에플리케이션 로딩 속도가 빨라진다. 
애플리케이션을 모두 한 파일에 패키징하면 클라인언트에서 단 한번만 HTTP요청을 보내면 된다. 
번들 안에 들어가는 코드를 축소하면 로딩시간을 더 줄일 수 있다.

- 일관성
웹팩이나 JSX나 자바스크립트를 컴파일해주기 때문에 프로젝트에서 아직 표준화 되지 않은 미래의 문법을 사용할 수 있다. 
바벨은 다양한 ESNext 문법을 지원하므로 브라우저가 여러분이 작성한 코드를 지원하지 않을까 염려할 필요가 없다. 
따라서 웹팩(그리고 바벨)을 사용하면 개발에 계속 최신 자바스크립트 문법을 활용할 수 있다.
```

## 5.5.1 프로젝트 설정하기
recipe-app 이라는 새로운 폴더를 만들고 진행하자.

```jsx
mkdir recipe-app
cd recipe-app
```

```jsx
# 순서
1. 프로젝트를 생성하다.
2. 조리법 앱을 컴포넌트로 나눠서 서로 다른 파일에 넣는다.
3. 바벨을 사용하는 웹팩 빌드를 설정한다.
```

### 1. 프로젝트 설정하기
```jsx
npm init -y
npm install react react-dom serve
```

다음으로는 각 컴포넌트를 담기 위해 아래와 같은 폴더 구조를 만든다.
```jsx
recipe-app(폴더)
  > node_modules (npm install 명령으로 자동 추가 됨)
  > package.json (npm init 명령으로 자동 추가 됨)
  > package-lock.json (npm init 명령으로 자동 추가 됨)
  > index.html
  > /src (폴더)
    > index.js
    > /data (폴더)
      > recipes.json 
    > /components (폴더)
      > Recipe.js
      > Instructions.js
      > Ingredients.js
```

### 2. 컴포넌트 모듈로 나누기
현재 Recipe 컴포넌트는 상당히 많은 일을 한다. 조리법 제목을 표시하고, 재료들의 ul을 만들고 조리 절차의 각 단계를 p로 만들어서 표시한다. 이 컴포넌트를 Recipe.js 파일에 넣어야 한다. JSX를 사용하는 파일마다 맨 위에 react를 임포트하는 문장이 필요하다.

```jsx
// ./src/components/Recipe.js

import React from "react";

export default function Recipe({name, ingredients, steps}){
  return (
    <section id="baked-salmon">
      <h1>{name}</h1>
      <ul className="ingredients">
        {ingredients.map((ingredient, i) => (
          <li key={i}>{ingredient.name}</li>
        ))}
      </ul>
      <section className="instructions">
        <h2>조리절차</h2>
        {steps.map((step, i) => (
          <p key={i}>{step}</p>
        ))}
      </section>
    </section>
  )
}
```

Recipe를 더 작고 담당하는 기능이 더 좁은 상태가 없는 여러 함수 컴포넌트로 분리한 다음에 그런 컴포넌트들을 합성하는 방식으로 처리하면 더 함수적인 접근 방식이 될 것이다. 먼저 조리 절차를 상태가 없는 함수 컴포넌트로 따로 분리하고 독립 파일에 모듈로 만들어서 어떤 절차든 표시할 수 있는 기능으로 분리하자.

Instructions.js라는 새 파일에 다음과 같이 컴포넌트를 넣자.

```jsx
// ./src/components/Instructions.js

import React from "react";

export default function Instructions({title, steps}){
  return(
    <section className="instructions">
      <h2>{title}</h2>
      {steps.map((s, i) => (
        <p key={i}>{s}</p>
      ))}
    </section>
  );
}
```

Instructions라는 새 컴포넌트를 만들었다, 이 컴포넌트는 절차의 제목과 각 단계를 인자로 받는다. 따라서 이 컴포넌트를 '조리법', '제빵법', '준비절차', '조리 전 체크리스트' 등 단계를 표시하는 다양한 경우에 사용할 수 있다.

이제 재료를 살펴보자. Recipe 컴포넌트에는 재료 이름만을 표시한다. 하지만 분량과 단위 정보도 재료 데이터에 존재한다. 이런 정보에 대한 Ingredient라는 컴포넌트를 만들자.

```jsx
// ./src/components/Ingredient.js

import React from "react";

export default function Ingredient({amount, measurement, name}){
  return(
    <li>
      {amount} {measurement} {name}
    </li>
  );
}
```

```jsx
// ./src/components/IngredientsList.js

import React from "react";
import Ingredient from "Ingredient";

export default function IngredientsList({list}){
  return(
    <ul className="ingredients">
      {list.map((ingredient, i) => (
        <Ingredient key={i} {...ingredient}/>
      ))}
    </ul>
  );
}
```

다음과 같이 스프레드 연사자를 사용하는 것은

```jsx
<Ingredient {...ingredient} />
```

다음과 같다.

```jsx
<Ingredient 
  amount={ingredient.amount}
  measurement={ingredient.measurement}
  name={ingredient.name}
/>
```

따라서 재료에 다음과 같은 필드가 있다면

```jsx
let ingredient = {
  amount: 1,
  measurement: 'cup',
  name: 'sugar'
}
```

다음과 같은 JSX 엘리먼트(컴포넌트)를 얻는다.

```jsx
<Ingredient 
  amount={1}
  measurement={cup}
  name={sugar}
/>
```

이제 재료와 조리 절체에 대한 컴포넌트를 만들었으므로 이런 컴포넌트를 합성해서 조리법을 만들 수 있다.

```jsx
// ./src/components/Recipe.js

import React from "react";
import IngredientsList from "./IngredientsList";
import Instructions from "./Instructions";

function Recipe({name, ingredients, steps}){
  return(
    <section id={name.toLowerCase().replace(/ /g, "-")}>
      <h1>{name}</h1>
      <IngredientsList list={ingredients} />
      <Instructions title="조리 절차" steps={steps} />
    </section>
  );
}

export default Recipe;
```

먼저 사용하려는 두 컴포넌트 IngredientsList와 Instructions를 임포트해여한다. 이제 이들을 사용해서 Recipe 컴포넌트를 만든다.  
한 함수 안에서 전체 조리법을 복잡하게 생성하는 대신에 작은 컴포넌트를 합성해서 좀 더 선언적인 방법으로 만들 수 있다.  
이 코드는 더 멋지고 간단할 뿐만 아니라 이해하기도 쉽다.  
이 코드를 보면 Recipe 컴포넌트가 조리법 이름을 표시하고 재료 목록과 절차를 표현하는 방법을 별도의 더 단순한 컴포넌트로 추상화해 표현한다.  
  
모듈화한 접근 방법에서 보면 Menu 컴포넌트도 상당히 비슷하다. 중요한 차이점은 Menu를 별도의 파일로 분리하고 필요한 다른 모듈을 임포트한 다음에 Menu 컴포넌트 즈신을 익스포트해야 한다는 점이다.

```jsx
// ./src/components/Menu.js

import React from "react";
import Recipe from "./Recipe";


function Menu({recipes}){
  return(
    <article>
      <header>
        <h1>맛있는 조리법</h1>
      </header>
      <div className="recipes">
        {recipes.map(({recipe, i}) => (
          <Recipe key={i} {...recipe} />
        ))}
      </div>
    </article>
  );
}
export default Menu;
```

```jsx
```

```jsx
```

```jsx
```

```jsx
```

## 출처
[]()