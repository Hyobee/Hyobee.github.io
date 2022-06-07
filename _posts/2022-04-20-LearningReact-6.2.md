---
title: "6.2 useState 훅"
permalink: /react/리액트상태관리/useState훅
categories:
  - React
tags:
  - Learning React
---

# 리액트 상태 관리

## 6.2 useState 훅
이제 StarRating 컴포넌트를 클릭할 수 있게 만들어야 한다.  
사용자는 컴포넌트를 클릭해서 rating을 바꿀 수 있다.  
**rating은 변경이 될 수 있는 값이기 때문에, 리액트 상태에 이 값을 저장하고 변경해야 한다.**
  
상태를 리액트 함수 컴포넌트에 넣을 때는 훅스(Hooks)라고 부르는 리액트 기능을 사용한다. 
훅스에는 컴포넌트 트리와 별도로 재사용 가능한 코드 로직이 들어있다.  
훅스를 사용하면 우리가 만든 컴포넌트에 기능을 끼워 넣을 수 잇다. 리액트는 몇가지 훅스를 기본 제공하므로, 즉시 이런 훅을 사용할 수 있다.  
  
우리가 가장 먼저 다룰 혹은, 상태를 리액트 컴포넌트에 추가하고 싶을 때 사용할 수 있는 리액트 **useState** 훅이다.   
이 훅은 실제로는 react 패키지에 들어있다. 따라서 react 패키지를 임포트 하기만하면 된다.

```jsx
import React, {useState} from "react";
import {FaStar} from "react-icons/fa";
```
사용자가 선택한 별의 개수는 별점을 표현한다.  
사용자가 선택한 별점을 저장하는 selectedStars라는 상태 변수를 만들 것이다.
useState 훅을 StarRating 컴포넌테 직접 추가해서 이 변수를 만든다.

```jsx
export default function StarRating({totalStars = 5}){
  const [selectedStars] = useState(3);
  return (
    <>
      {createArray(totalStars).map((n, i) => (
        <Star key={i} selected={selectedStars > i} />
      ))}
      <p>
        {selectedStars} / {totalStars}
      </p>
    </Star>
  );
}
```

방금 컴포넌트와 상태를 서로 엮었다(Hooked).  
userState 훅은 배열을 반환하는 호출 가능한 함수이다.  
이 배열의 첫 번째 값이 우리가 사용하려는 상태 변수다. 여기서는 이 변수가 selectedStars이고, 이 변수의 값은 StarRating에서 빨간색으로 칠해야 하는 별의 개수이다.  
useState는 배열을 반환한다. 배열 구조 분해를 활용하면 쉽게 상태 변수에 이름을 붙일 수 있다.  
useState 함수에 전달하는 값은 상태 변수의 디폴트 값이다. 여기서는 selectedStars 의 초기값이 3으로 설정된다.
  
사용자로부터 다른 점수를 얻기 위해서는 사용자가 아무 별이나 클릭할 수 있게 해야 한다.  
이 말은 onClick 핸들러를 FaStars 컴포넌트에 추가해서 별을 클릭할 수 있게 만들어야 한다는 뜻이다. 

```jsx
const Star = ({selected = false, onSelect = f => f}) => (
  <FaStar color = {selected ? "red" : "grey"} onClick={onSelect} />
);
```
Star를 변경해서 onSelect라는 프로퍼티를 추가한다.  
이 프로퍼티가 함수라는 점에 유의하자. 사용자가 FaStar 컴포넌트를 클릭하면 이 함수를 호출할 것이다.  
이 함수는 부모 컴포넌트에게 별이 클릭됐음을 통지한다.  
이 함수의 디폴트 값은 f => f 이다.  
이 함수는 인자로 받은 값을 그대로 돌려주는 일 외에 아무 일도 않는 가짜 함수일 뿐이다.
하지만 onSelect 프로퍼티의 값은 반드시 함수여야 하므로 onSelect에 함수를 지정하지 않고 FaStar 컴포넌트를 클릭하면 오류가 발생한다. 
  
비록 f => f 가 아무일도 하지 않지만, 이 함수도 함수이기 때문에 아무 오류를 발생시키지 않고 호출 될 수 있다.
따라서 이제는 상위 컴포넌트에서 Star를 만들면서 onSelect 프로퍼티를 별도로 지정하지 않아도 아무 문제도 없다.
리액트는 가짜 함수를 호출하고도 아무 일도 발생하지 않을 것이다.

이제 Star 컴포넌트를 클릭할 수 있으므로, 이 성질을 활용해 StarRating의 상태를 바꿔보자.

```jsx
export default function StarRating({totalStars= 5}){
  const [selectedStars, setSelectedStars] = useState(0);
  return (
    <>
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
    </>
  );
}
```

StarRating 컴포넌트의 상태를 바꾸려면 selectedStars의 값을 바꾸는 함수가 필요하다.
useState 훅이 반환하는 배열의 두 번째 원소는 상태 값을 변경할 때 쓸 수 있는 함수다.  
이 경우도 배열을 구조 분해해서 함수에 원하는 이름을 붙일 수 있다.
이 함수가 selectedStars의 값을 설정하기 때문에 함수의 이름을 setSelectedStars라고 정했다.
  
훅스에서 기억할 가장 중요한 내용은 훅이 걸린 컴포넌트를 렌더와 연동시킨다는 점이다.
setSelectedStars 함수를 사용해 selectStars의 값을 바꿀 때마다 StarRating 함수 컴포넌트가 훅에 의해 다시 호출되면서 렌더링이 다시 이루어 진다.
훅스가 그렇게 중요하고 유용한 기능이 될 수 있는 이유가 바로 이것이다.
훅이 걸린 데이터가 변경되면 데이터에 대한 훅이 걸린 컴포넌트에 새 값을 전달하면서 컴포넌트를 다시 렌더링해준다.
  
사용자가 Star를 클릭할 때마다 StarRating 컴포넌트가 다시 렌더링 된다.  
사용자가 Star를 클릭하면 해당 Star의 onClick 프로퍼티가 호출된다. 
onSelect 프로퍼티는 setSelectedStars 함수를 호출해서 방금 선택한 별의 개수를 전송한다.  
map함수의 i변수를 사용해 개수를 쉽게 계산할 수 있다. map이 첫 번째 Star를 렌더링할 때 i의 값은 0이다. 
따라서 i에 1을 더해서 올바른 별의 개수를 얻을 수 있다.  
setSelectedStars가 호출되면서 새로운 selectedStars 값을 사용해 StarRating 컴포넌트가 호출된다.

리액트 개발자 도구는 어떤 컴포넌트에 어떤 훅이 걸려있는지 보여준다.  
StarRating 컴포넌트를 브라우저에서 렌더링할 때는, 개발자 도구에서 해당 컴포넌트를 선택하여 디버깅 정보를 살펴 볼 수 있다.  
오른쪽이 열에서 StarRating 컴포넌트에 State 훅이 잇고 그 훅의 값이 2라는 사실을 알 수 있다.  
앱과 상호작용하면 상태값이 변하고 그 별 개수에 상응하는 컴포넌트의 트리가 다시 렌더링되는 모습을 볼 수 있다.


## 완성코드

```jsx
import React, {useState} from "react";
import {FaStar} from "react-icons/fa";

export default function StarRating({totalStars= 5}){
  const [selectedStars, setSelectedStars] = useState(0);
  const createArray = length => [...Array(length)];
  const Star = ({selected = false, onSelect = f => f}) => (
    <FaStar color = {selected ? "red" : "grey"} onClick={onSelect} />
  );

  return (
    <>
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
    </>
  );
}
```

## 완성 코드 출처
[Star Rating - Component State](https://github.com/enshahar/learning-react-kor/tree/seconded/chapter-06)