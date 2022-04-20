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
<h1>{title.toLowerCase().replace}</h1>
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
data 배열 속 프로퍼티(name, ingredients, step) 전체를 일일히 한땀 한땀 불러옴. 
**스프레드 연산자**를 통해 전체를 불러올 수 있다.
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

### Menu 내 recipe component 개선 (스프레드 연산자)
```jsx
{
  props.recipe.map((recipe, i) => 
    <Recipe key={i} {...recipe} />
  );
}
```

**스프레드 연산자**는 recipe 객체의 각 필드를 Recipe 컴포넌트의 프로퍼티(name, ingredients, step)로 추가해준다.    
이런 단축 표기법은 모든 프로퍼티(name, ingredients, step)를 Recipe 컴포넌트에게 제공한다.
이런 기능이 좋을 때도 있지만 컴포넌트에 너무 많은 프로퍼티를 추가하게 될 수도 있다.

### Menu component 개선 (객체 구조분해)
Menu component를 개선시킬 수 있는 다른 부분으로는 props인자를 받는 부분이 있다. **객체 구조분해**를 사용하면 이 함수 내부로 변수 영역을 한정시킬 수 있다. 이렇게 하면 직접 title과 recipe를 사용할 수 있고 항상 props를 덧붙여야하는 번거로움을 줄일 수 있다.

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
현재 Recipe 컴포넌트는 상당히 많은 일을 한다. 조리법 제목을 표시하고, 재료들의 ul을 만들고 조리 절차의 각 단계를 li로 만들어서 표시한다. 이 컴포넌트를 Recipe.js 파일에 넣어야 한다. JSX를 사용하는 파일마다 맨 위에 react를 임포트하는 문장이 필요하다.

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

다음과 같이 스프레드 연산자를 사용하는 것은

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

먼저 사용하려는 두 컴포넌트 IngredientsList와 Instructions를 임포트해야한다. 이제 이들을 사용해서 Recipe 컴포넌트를 만든다.  
한 함수 안에서 전체 조리법을 복잡하게 생성하는 대신에 작은 컴포넌트를 합성해서 좀 더 선언적인 방법으로 만들 수 있다.  
이 코드는 더 멋지고 간단할 뿐만 아니라 이해하기도 쉽다.  
이 코드를 보면 Recipe 컴포넌트가 조리법 이름을 표시하고 재료 목록과 절차를 표현하는 방법을 별도의 더 단순한 컴포넌트로 추상화해 표현한다.  
  
모듈화한 접근 방법에서 보면 Menu 컴포넌트도 상당히 비슷하다. 중요한 차이점은 Menu를 별도의 파일로 분리하고 필요한 다른 모듈을 임포트한 다음에 Menu 컴포넌트 자신을 익스포트해야 한다는 점이다.

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
Menu 컴포넌트를 렌더링할때도 여전히 ReactDOM을 사용해야 한다. 
프로젝트의 주 파일은 여전히 index.js이다. 이 파일이 DOM에 컴포넌트를 렌더링한다.
이 파일을 만들어 보자. 

```jsx
// ./src/index.js

import React from "react";
import {render} from "react-dom";
import Menu from "./components/Menu";
import data from "./data/recipe.json";

render(<Menu recipes={data}>, document.getElementById("root"));
```

맨 앞 네 문장은 이 앱이 작동하는데 필요한 모듈을 임포트한다.  
react와 react-dom을 script 태그에서 임포트하는 대신 여기서 그 둘을 임포트해서 웹팩이 번들에 그 두 라이브러리를 추가하도록 만든다. 또한 Munu컴포넌트와 예제 데이터 배열을 임포트해야 한다.  
예제 데이터 배열도 별도의 모듈로 분리했다. 그 안에는 '구운연어'와 '생선타코' 조리법이 들어 있다.
  
임포트한 변수들은 index.js 파일 안에서만 볼 수 있다. Menu 컴포는터를 렝더링할 때 조리법 데이터 배열을 Menu의 프로퍼티로 전달한다.
  
데이터는 recipe.json 파일에서 가져온다. 이번 장 앞에서 사용했던 데이터와 같은 데이터를 사요하되, 제대로된 JSON 형식을 지켜 작성한다.

```jsx
[
  {
    "name": "구운 연어",
    "ingredients": [
      { "name": "연어", "amount": 500, "measurement": "그램" },
      { "name": "잣", "amount": 1, "measurement": "컵" },
      { "name": "버터 상추", "amount": 2, "measurement": "컵" },
      { "name": "옐로 스쿼시(Yellow Squash, 호박의 한 종류)", "amount": 1, "measurement": "개" },
      { "name": "올리브 오일", "amount": 0.5, "measurement": "컵" },
      { "name": "마늘", "amount": 3, "measurement": "쪽" }
    ],
    "steps": [
      "오븐을 350도로 예열한다.",
      "유리 베이킹 그릇에 올리브 오일을 두른다.",
      "연어, 마늘, 잣을 그릇에 담는다.",
      "오븐에서 15분간 익힌다.",
      "옐로 스쿼시를 추가하고 다시 30분간 오븐에서 익힌다.",
      "오븐에서 그릇을 꺼내서 15분간 식힌다음에 상추를 곁들여서 내놓는다."
    ]
  },
  {
    "name": "생선 타코",
    "ingredients": [
      { "name": "흰살생선", "amount": 500, "measurement": "그램" },
      { "name": "치즈", "amount": 1, "measurement": "컵" },
      { "name": "아이스버그 상추", "amount": 2, "measurement": "컵" },
      { "name": "토마토", "amount": 2, "measurement": "개(큰것)"},
      { "name": "또띠야", "amount": 3, "measurement": "개" }
    ],
    "steps": [
      "생선을 그릴에 익힌다.",
      "또띠야 3장 위에 생선을 얹는다.",
      "또띠야에 얹은 생선 위에 상추, 토마토, 치즈를 얹는다."
    ]
  }
]
```

## 3. 웹팩 빌드 만들기
웹팩으로 정적인 빌드 프로세스를 만들려면 몇몇 모듈을 설치해야 한다. npm을 사용해 필요한 모든 모듈을 설치할 수 있다.

```jsx
npm install --save-dev webpack webpack-cli
```

모듈화한 조리법 앱이 작동하게 만들려면 소스 코드를 어떻게 한 번들 파일로 만들 수 있는지 웹팩에게 알려줘야 한다.
웹팩 버전 4.0.0 부터는 프로젝트를 번들하기 위해 설정 파일을 만들 필요가 없어졌다. 설정 파일이 없으면 웹팩이 코드를 패키징 하기 위한 디폴트 방식을 사용한다. 하지만 설정파일을 사용하면 설정을 원하는 대로 커스텀화할 수 있다. 게다가 설정 파일이 있으면 웹팩의 마법을 감추는 대신 명시저긍로 볼 수 있다. 디폴트 웹팩 설정 파일은 항삭 webpack.config.js이다.

조리법 앱의 시작 파일은 index.js 이다. index.js는 React, ReactDOM, Menu.js 파일을 임포트한다. 브라우저에서 가장 먼저 실행해야하는 부분이 바로 이부분이다. 웹팩은 import문을 발견할 때마다 파일시스템에서 해당 모듈을 찾아서 번들에 포함시켜준다.
index.js는 Menu.js를 임포트하고 Menu.js는 Recipe.js를 임포트하며 Recipe.js는 Instrunctions.js와 IngredientsList.js를 임포트하고, IngredientsList.js는 Ingredient.js를 임포트한다.
웹팩은 이런 임포트 트리를 쫒아가면서필요한 모듈을 모두 번들에 넣어준다. 이 모든 파일을 순회하면 의존관계 그래프가 생긴다.
의존 관계는 컴포넌트 파일이나 리액트와 같은 라이브러리 파일, 이미지 등 앱에게 필요한 요소를 뜻한다.
그래프에서 각각의 파일을 원으로 표현한다면, 웹팩은 그래프를 만들기 위해 원과 원 사이에 선을 그어준다. 그리고 이렇게 만들어진 그래프가 전체 번들이다.

```
**import문**
조리법 앱은 import 문을 사용하지만 노드나 현재 사용중인 대부분의 브라우저는 이를 지원하지 않는다. 그럼에도 불구하고 import문이 작동할 수 있는 이유는 바벨이 import를 require('모듈/경로')로 변환하기 때문이다. require 함수는 일반적으로 커먼 js에서 모듈을 임포트할 떄 사용하는 함수이다.
```

웹팩이 번들을 빌드할 때, JSX를 순수 리액트 코드로 변환하라고 지정할 필요가 있다.

webpack.config.js 파일은 웹팩이 수행해야 하는 동작을 기술하는 자바스크립트 리터럴을 익스포트하는 모듈에 지나지 않는다. 이 설정 파일은 index.js 파일이 있는 프로젝트 루트 폴더에 저장되야 한다.

```jsx
// ./webpack.config.js

var path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "dist", "assets"),
    filename: "bundle.js"
  }
};
```
우선 웹팩에게 클라이언트의 시작 파일이 ./src/index.js라는 사실을 지정한다 웹팩은 그 파일안에 있는 import 문부터 시작해서 모든 의존 관계 그래프를 자동으로 만든다. 다음으로 번들을 ./dist/bundle.js라는 자바스크립트 파일에 출력하라고 지정한다. 웹팩은 이 위치에 패키징한 자바스크립트 파일을 넣어준다.
  
다음으로 필요한 바벨 의존 관계를 설치하자. babel-loader와 @babel/core가 필요하다.

```jsx
npm install babel-loader @babel/core --save-dev
```

이 다음에 필요한 명령은 특정 모듈을 실행할 때 사요할 로더 목록이다. 설정 파일에서 module이라는 필드 안에 이런 정보를 추가한다.

```jsx
module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "dist", "asset"),
    filename: "bundle.js",
  }
  module: {
    rules: [{test: /\.js$, exclude: /node_modules/, loader: babel-loader}]
  }
};
```

rules 필드는 웹팩에 사용할 여러 유형의 로더를 포함해야 하기 때문에 배열이다. 이 예제에서는 babel-loader만 포함시켰다. 
각 로더는 자바스크립트 객체다. test 필드는 각 모듈에서 로더가 작용해야 하는 파일 경로를 찾기 위한 정규식이다.
이 예제에서는 node_modules 폴더에서 찾은 자바스크립트 파일이 아닌 모든 자바스크립트 파일에 대해 babel-loader를 실행한다.

이 시점에서 바벨을 실핼할 때 사용할 프리셋을 지정해야 한다. 프리셋을 지정하면 바벨에게 어떤 식으로 파일을 변환할지 알려주게 된다. 다른 말로 하면, 이를 통해 "바벨, 이 프로젝트에서 ESNext구문을 보면 코드를 브라우저가 이해할 수 있는 구문으로 변환하고 계속 진행 해줘" 리고 요구할 수 있다. 먼저 프리셋을 먼저 설치해야 한다.

```jsx
npm install @bable/preset-env @babel/preset-react --save-dev
```
추가로 프로젝트 루트에 .babelrc라는 파일을 만들자.

```jsx
"presets": ["@babel/preset-env", "@babel/preset-react"]
```
지금까지 실제 리액트 앱을 닮은 프로젝트를 만들었다. 더 진행해서 웹팩을 실행하면서 이 설정이 제대로 작동하나 살펴보자.

웹팩은 정적으로 실행된다. 보통 앱을 서버에 배포하기 전에 번들을 만든다. npx라는 명령을 사용하면 명령줄에서 webpack을 실행할 수 있다.

```jsx
npx webpack --mode development
```
웹팩은 성공해서 번들을 만들거나 실패해서 오류 메세지를 표시한다. 대부분의 오류는 임포트 참조가 잘못된 경우 발생한다. 웹팩 오류를 디버길할 때는 import문에 사용한 파일 이름과파일 경로를 자세히 살펴봐야 한다.

package.json 파일에 npm 스크립트를 추가해서 npm을 통해 웹팩을 간편하게 실행하는 지름 길을 만들 수도 있다.

```jsx
"script": {
  "build": "webpack --mode production"
},
```

지름길 스크립트를 추가한 다음에는 이 지름길을 사용해 번들을 생성하는 명령을 내릴 수 있다.

```jsx
npm run build
```

## 5.5.2 번들 로딩하기
번들을 만들었다. 이제 뭘할 수 있을까? 웹팩은 번들을 dist 폴더에 넣는다. 이 폴더ㅗ에는 웹 서버에서 번들을 실핼할 때 필요한 파일들이 들어있다. dist총더에는 index.html파일이 포함되어야 한다. 
index.html 파일이 있어여 리액트 Menu 컴포넌트를 마운트시킬 대상 div 엘리먼트를 찾을 수 있다.
index.html 파일에는 방금 만들 번들을 로딩하기 위한 script 태그도 들어있다.

```jsx
// ./src/index.html

<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>리액트 조리법</title>
</head>
<body>
  <div id="root"></div>
  <script src="assets/bundle.js"></script>
</body>
</html>
```

이 페이지가 조리법 앱의 홈페이지다. 이 페이지는 한 파일 bundle.js에 대한 HTTP 요청을 보냄으로 필요한 모든 자원을 로딩한다. dist안에 있는 파일들을 웹 서버에 배포하거나 노드나 루비 온 레일즈 같은 웹서버 어플리케이션을 통해 파일을 HTTP프로토콜로 서비스해야 한다.

## 5.5.3 소스맵
코드를 한 번들 파일로 만들면 브라우저에서 앱을 디버깅할 때 약간 곤란해진다.
이런 문제를 소스맵을 통해 해결할 수 있다. 소스 맵은 번들과 소스 파일을 연결해주는 파일이다.
웹팩에서는 webpack.config.js 파일에 몇 줄 추가하면 ㅇ런 소스 매핑을 추가할 수 있다.

```jsx
module.exports = {
  ...
  devtool: '#source-map' // 소스맵을 추가하려면 이 옵션을 덧붙여라
};
```

devtool 프로퍼티를 #source-map으로 설정하면 웹팩이 소스 매핑을 사용하게 할 수 있다.
다시 웹팩을 실행하면 assets 폴더에[ bundle.js와 bundle.map이라는 두 파일이 생긴다.
  
소스맵은 디버깅시 원 소스 코드를 사용할 수 있게 해준다. 브라우저의 개발자 도구에 있는 소스맵에서 webpack://이라고 쓰인 폴더를 찾을 수 있을 것이다. 그 폴더 안에는 번들에 들어있는 모든 소스 파일이 보여야 한다.
  
브라우저 디버거의 단계별 실행 기능을 활용해 이런 소스 파일을 디버깅할 수 있다. 소스코드 옆의 행 번호를 클릭하면 중단점을 설정할 수 있다. 브라우저를 새로고침하면 자바스크립트를 새로 실행하다가 아무 중단점이나 만나면 실행이 일시 중단된다. 영역 패널에서 각 영역에 속한 변수를 살펴보거나 감시 패널에 변수이름을 입력해 값을 추적할 수 있다.
  
##5.5.4 create-react-app
이 도구는 리액트 프로젝트를 생성하는 명령줄 도구이다. 개발자들이 직접 웹팩, 바벨 등 여러도구의 설정을 손보지 않아도 빠르게 리액트프로젝트를 시작할 수 있다.
패키지를 글로벌로 설치해야 사용가능하다.

```jsx
npm install -g create-react-app
```
설치 후 create-react-app 명령과 앱을 생성할 폴더의이름을 지정하면 앱을 만들 수 있다.

```jsx
create-react-app myproject
```

```
npx를 사용하면 글로벌 설치를 하지 않아도 create-react-app을 호출할 수 있다.
단지 npx create-react-app my-project를 실행하자. 
```

이 명령은 리액트 프로젝트를 my-project 폴더에 만들면서 React, ReactDOM, react-scripts에 대한 의존 관계를 설정해준다. react-scripts는 바벨 ESLint, 웹팩 등을 설치해서 개발자가 직접 그런 도구를 설정할 필요가 없게해준다.
생성된 프로젝트 폴더 안에는 App.js파일이 들어있는 src 폴더가 있다.
App.js 파일에서 루트 컴포넌트를 수정하거나 다른 컴포넌트 파일을 임포트할 수 있다.
  
조금 전에 만든 my-project 폴더를 현재 폴더를 만든 후, npm start를 실행할 수 있다.
yarn start를 실행할 수도 있다. 이런 명령들은 애플리케이션을 3000번 포트에서 실행한다.
  
npm test나 yarn test를 통해 테스트를 실행할 수도 있다. yarn의 경우에는 yarn build를 하자, 이 명령은 변환과 축소를 거친 프로덕션에 사용할 수 있는 번들을 만든다.