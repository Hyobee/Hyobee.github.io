---
title: "6.3 재사용성을 높이기 위한 리팩터링"
permalink: /react/리액트상태관리/재사용성을높이기위한리팩터링
categories:
  - React
tags:
  - Learning React
---

# 리액트 상태 관리

## 6.3 재사용성을 높이기 위한 리팩터링

이제 Star 컴포넌트를 프로덕션에 넣어도된다. 사용자에게 평점을 받을 필요가 있는 여러 애플리케이션에서 이 컴포넌트를 사용할 수 있다.
하지만 이 컴포넌트를 npm에 올려서 세상 누구나 사용자로부터 평점을 받을 대 이 컴포넌트를 활용하게 하고 싶다면, 몇가지 용례를 더 생각해봐야 한다.
  
첫 째로, style 프로퍼티를 생각해보자. 이 프로퍼티를 사용하면 css스타일을 엘리먼트에 추가할 수 있다.  
나중에 개발자가, 심자어 여러분 자신일 수 있다. 전체 컨테이너의 스타일을 변경해야 할 수도 있다. 이런경우 다음과 비슷한 방법을 시도할 것이다.

```jsx
export default function App(){
  return <StarRating style={{backgroundColor: "lightblue"}} />;
}
```

```jsx
import React, {useState} from "react";
import {FaStar} from "react-icons/fa";

export default function StarRating({style={}, totalStars= 5, ...props}){
  const [selectedStars, setSelectedStars] = useState(0);
  const createArray = length => [...Array(length)];
  const Star = ({selected = false, onSelect = f => f}) => (
    <FaStar color = {selected ? "red" : "grey"} onClick={onSelect} />
  );

  return (
    <div style={{padding: "5", ...style}} {...props}>
      {createArray(totalStars).map((n, i) => (
        <Star 
          key={i}
          selected={selectedStars > i}
          onSelect={() => setSelectedStars(i + 1)}
        />
      ))}
      <p>
        {selectedStars} / {totalStars}
      </p>
    </div>
  );
}
```

```jsx
```

```jsx
```

## 출처
[]()