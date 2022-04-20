---
title: "6.4 컴포넌트 트리 안의 상태"
permalink: /react/리액트상태관리/컴포넌트트리안의상태
categories:
  - React
tags:
  - Learning React
---

# 리액트 상태 관리

## 6.4 컴포넌트 트리 안의 상태

상태를 한 곳에서 관리하는 방법에는 몇 가지가 있다. 
상태를 컴포넌트 트리에 저장하고, 자식 컴포넌트들에게 프롭으로 전달하는 방법이다.
  
색의 목록을 관리하는 작은 애플리케이션을 만들어 보자. 이 앱을 "색의 관리자" 라고 부른다.
이 앱은 사요자가 목록에 있난 색에 대해 별점과 제목을 부여할 수 있게 한다.  
출발점으로 다음과 같은 간단한 데이터 집합이 있다.

```jsx
{
  colors: [
    {
      "id": "0175d1f0-a8c6-41bf-8d02-df5734d829a4",
      "title": "ocean at dusk",
      "color": "#00c4e2",
      "rating": 5
    },
    {
      "id": "83c7ba2f-7392-4d7d-9e23-35adbe186046",
      "title": "lawn",
      "color": "#26ac56",
      "rating": 3
    },
    {
      "id": "a11e3995-b0bd-4d58-8c48-5e49ae7f7f23",
      "title": "bright red",
      "color": "#ff0000",
      "rating": 0
    }
  ]
}
```

color-data.json 파일에는 3가지 색으로 이뤄진 배열이 들어있다.
각 색에는 id, title, color, rating이 있다. 
먼저 이 데이터를 브라우저에 표시할 리액트 컴포넌트로구성된 UI를 만들자. 
그 후 사용자가 새로운 리스트에 색을 추가하거나, 삭제하고, 색에 평점을 매길 수 있게 하자.

## 6.4.1 상태를 컴포넌트 트리의 아래로 내려보내기

이번 리터레이션에서는 상태를색관리자 앱의루트인 App 컴포넌트에 저장한다.
그리고 색을 자식 컴포넌트로내려보내서 렌더링 한다.
App 컴포넌트는 우리 앱에서 상태를 저장할 유일한 컴포넌트다.
useState 훅을 사용해 App에 색 리스트를 추가한다.

```jsx
import React, {useState} from "react";
import ColorData from "./color-data.json";
import ColorList from "./ColorList.js";

export default function App(){
  const [colors] = useState(colorData);
  return <ColorList colors={colors} />;
}
```

App 컴포넌트는 트리의 최상위에 있다. 
useState를 이 컴포넌트에 추가하면 색의 상태 관리를 App과 연결한다. 
이 예제에서 colorData는 앞에서 본 예제 색의 배열이다. 
App 컴포넌트는 colorDat를 colors의 초기 상태로 사용한다. 
App으로부터 colors가 ColorList라는 컴포넌트에게 전달된다.

```jsx
import React from "react";
import Color from "./Color";

export default function ColorList({colors=[]}){
  if(!colors.length) return <div>표시할 색이 없습니다.</div>;

  return (
    <div>
      {
        colors.map(color => <Color key={color.id} {...color} />)
      }
    </div>
  );
}
```

ColorList는 프롭으로 App컴포넌트에게 색을 전달받는다.  
colors가 비어 있으면 컴포넌트는 사용자에게 메세지를 표시한다.   
colors에 색 배열이 있으면 이 배열에 대해 map을 수행해서   
s세부정보를 Color로 만들면서 트리의 아래 방향으로 각 색 정보를 내려 보낸다.

```jsx
export default function Color({title, color, rating}){
  return (
    <section>
      <h1>{title}</h1>
      <div style={{height: "50", backgroundColor: color}} />
      <StarRating selectedStars={rating}/>
    </section>
  );
}
```

Color 컴포넌트는 title, color, rating 이라는 세 프로퍼티를 받는다.  
각 값은 <Color {...color} />를 통해 스프레드 연산자로 전달 받는다. 이 식은 color 객체에 있는 각 필드를 color 객체의 각 키와 똑같은 키를 가지는 프로퍼티로 Color 컴포넌트에 전달한다.
Color 컴포넌트는 이렇게 받은 값을 표시한다. 
title은 h1엘리먼트 안에 표시하고, color 값은 div 엘리먼트의 backgroundColor로 표시하며, rating은 트리의 아래에 있는 StarRating 컴포넌트에게 전달한다.
StarRating 컴포넌트는 이 rating 값을 선택된 별의 개수로 표시해준다.

```jsx
export default function StarRating({totalStars = 5, selectedStars = 0}){
  return (
    <>
      {createArray(totalStars).map((n, i)=> (
        <Star
          key={i}
          selected={selectedStars > i}
        />
      ))}
      <p>
        {selectedStars} / {totalStars}
      </p>
    </>
  );
}
```

앞 절에서 본 StarRating 컴포넌트를 약간 변경했다는 점에 유의하자.
StarRating 컴포넌트를 순수 컴포넌트로 변경했다.  
순수컴포넌트는 상태가 없기 때문에 항상 같은 프롭에 대해 같은 사용자 인터페이스를 렌더링 해주는 컴포넌트를 말한다.
색 별점 상태가 컴포넌트 트리의 루트에 있느느colors 배열에 저장되어 있기 때문에 컴포넌트를 순서 컴포넌트로 만들었다.
이번 이터레이션의 목적이 상태를 한 장소에만 저장하고 트리상의 여러 컴포넌트에 분산하지 않는 것이라는 점을 기억하자.

```
컴포넌트가 자체적으로 상태를저장하면서프롭을 통해 상태를 전달받을 수도 있다.
커뮤니티에서 널리 쓰일 수 있게 컴포넌트를 배로하려면 보통리런 식의 동작이 필요하다.
이런 기업의 예를 다음 장에서 useEffect 훅을 다룰 때 살펴본다.
```

이제 상태를 App 컴포넌트에서 컴포넌트 트리의 아래로 내려보내서 결국 Star 컴포넌트가 각 색에 해당하는 rating 값에 맞춰 자신을 색칠하게 만들었다.
앞에서 본 color-data.json에 따라 이 앱을 렌더링해 브라우저에서 실행해보자.

```jsx
```

```jsx
```

## 출처
[]()