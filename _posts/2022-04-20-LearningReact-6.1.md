---
title: "6.1 리액트 상태 관리"
permalink: /react/리액트상태관리/별점컴포넌트만들기
categories:
  - React
tags:
  - Learning React
---

# 리액트 상태 관리
사용자 인터페이스는 콘텐츠 생산자가 콘텐츠를 만들어 내기 위해 사용하는 도구이다.  
콘텐츠 생산자에게 최선의 도구를 만들어내기 위해서는 **데이터를 효율적으로 조작하고 변경하는 방법**을 알아야 한다.
  
5장에서는 컴포넌트 트리를 만들었다. 
**컴포넌트 트리**는 프로퍼티를 통해 데이터가 흘러갈 수 있는 **컴포넌트 계층 구조**를 뜻한다.  
프로퍼티는 전체 그림에서 절반에 불과하다. **상태(state)**가 나머지 절반이다.  
리액트 애플리케이션의 상태는 데이터에 의해 조정되며 변경될 수 있다.
상태를 조리법 애플리케이션에 도입하면 셰프가 새 조리법을 만들 수도 있고, 기존 조리법을 변경하거나 오래된 조리법을 제거할 수도 있다.
  
상태와 프로퍼티는 서로 관계가 있다. 리액트 애플리케이션을 사용할 때는 이 관계에 기반해 컴포넌트들을 부드럽게 합성해 서로 엮는다.
컴포넌트 트리의 상태가바뀌면 프로퍼티도 바뀐다. 새로운 데이터는 컴포넌트 트리를 타고 흐르고, 콘텐츠에 반영되도록 특정 말단이나 가지가 다시 렌더링 된다.
  
이번 장에서는 **상태**를 도입함으로써 애플리케이션에 생명을 불어넣는다.  
```
1. 상태가 있는 컴포넌트를 만드는 방법을 배우고,  
2. 컴포넌트 트리 아래 방향으로 상태를 전달하는 방법과 사용자 상호작용을 컴포넌트 트리의 위쪽으로 돌려보내는 방법을 살펴본다.  
3. 사용자로부터 폼 데이터를 얻는 기술도 배운다.  
4. 그리고 상태가 있는 콘텍스트 프로바이더를 통해 애플리케이션에서 관심사를 분리하는 방법에 대해 살펴본다.
```

## 6.1 별점 컴포넌트(Star Rating Component) 만들기

- StarRating 컴포넌트를 통해 사용자는 콘텐츠에 별의 개수를 바탕으로 점수를 매길 수 있다.    
- 좋지 않은 콘텐츠는 별을 하나만 받는다.  
- 아주 권장할 만한 콘텐츠는 별을 다섯 개 받는다.   
- 사용자는 별을 클릭해서 콘텐츠의 별점을 지정할 수 있다.  
먼저 별점이 필요하다. react-icon에서 별을 얻을 수 있다.

```jsx
npm i react-icons
```

## CRA시 issue 발생
리액트 프로젝트 설치를 위해 create-react-app star-rating을 실행했지만, 프로젝트가 생성이 안되는 이슈가 발생.  
아래와 같은 오류 메시지 터미널에 발생.

### issue 발생 이유
npm 버전 문제로 인해 발생. 

```jsx
You are running `create-react-app` 4.0.2, which is behind the latest release (4.0.3)
```
npx 대신 yarn을 사용할 수도 있다.

```
1. npm uninstall -g create-react-app
2. npm add create-react-app
3. 다시 npx create-react-app myapp
```

### CRA issue 해결하는데 도움받은 링크
[React 오류 해결 You are running `create-react-app` 4.0.2, which is behind the latest release (4.0.3).](https://velog.io/@milkyway/React-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0-You-are-running-create-react-app-4.0.2-which-is-behind-the-latest-release-4.0.3)


```jsx
import React from "react";
import {FaStar} from "react-icons/fa";

export default function StarRating(){
  return [
    <FaStar color="red" />,
    <FaStar color="red" />,
    <FaStar color="red" />,
    <FaStar color="grey" />,
    <FaStar color="grey" />
  ];
}
```

이 코드는 react-icon에서 임포트한 SVG 별을 다섯개 렌더링하는 StarRating 컴포넌트를 만든다.  
앞의 세 별은 빨간색으로 채워지고, 뒤의 두 별은 회색으로 채워진다. 별을 먼저 렌더링하는 이유는 앞으로 우리가 만들어나갈 컴포넌트에 대한 길잡이를 제공하기위해서다. 선택된 별은 빨간색으로 칠해져야 하고, 선택받지 못한 별은 회색으로 표시되어야 한다.
선택된 프로퍼티에 따라 자동으로 별을 만들어내는 컴포넌트를 하나 만들자.

```jsx
const star = ({selected = false}) => (
  <FaStar color={selected ? "red" : "grey"} />
);
```

Star 컴포넌트는 별 하나를 렌더링 한다. 이 떄 selected 프로퍼티에 따라 적절한 색으로 별 안쪽을 채워넣는다.  
selected 프로퍼티가 컴포넌트에 전달되지 않으면 별이 선택되지 않는다고 가정하고, 디폴트로 회색으로별 내부를 칠한다.
  
개발자가 자신의 앱에 별점 컴포넌트를 추가할 때 원하는 대로 별의 개수를 정할 수 있게 해야 한다.  
totalStars 프로퍼티를 StarRating 컴포넌트에 추가해서 전체 별 개수를 지정할 수 있게 해야한다.

```jsx
const createArray = length => [...Array(length)];

export default function StarRating({totalStars = 5}){
  return createArray(totalStars).map((n, i) => <Star key = {i}>);
}
```
### createArray
여기서는 2장에서 배운 **createArray** 함수를 사용한다.  
생성하려는 배열의 원소 개수를 지정하기만 하면 원하는 기수의 원소가 들어있는 배열을 얻을 수 있다.  
  
이 함수를 totalStars 프로퍼티와함께 사용하면 원하는 길이의 배열을 얻을 수 있다. 배열이 생기면 그 배열에 대해 map을 수행하면서 Star 컴포넌트를 렌더링한다. 디폴트로 totalStars는 5이다. 이 말은 이 컴포넌트가 기본적으로 5개의 별을 렌더링 한다는 뜻이다.
