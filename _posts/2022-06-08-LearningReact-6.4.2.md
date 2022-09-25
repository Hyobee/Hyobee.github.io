---
title: "6.4.2 상호작용을 컴포넌트 트리 위쪽으로 전달하기"
permalink: /react/리액트상태관리/상호작용을컴포넌트트리위쪽으로전달하기
categories:
  - React
tags:
  - Learning React
---

# 리액트 상태 관리

## 6.4.2 상호작용을 컴포넌트 트리 위쪽으로 전달하기

지금까지는 리액트 컴포넌트를 합성하고 데이터를 부모 컴포넌트에서 자식 컴포넌트에게 내려 보내는 방식으로 컴포넌트 트리 아래쪽으로 돌려보냄으로써 colors 배열을 렌더링 했다.  
리스트에서 색을 제거하거나 리스트에 들어 있는 색의 평점을 변경하면 어떤 일이 생길까?  
  
colors는 트리의 루트에 들어있다. 따라서 자식 컴포넌트에 대해 벌어지 상호작용을 수집해서 트리의 위로 올려보내서 상태가 저장된 루트 컴포넌트에 도착하게 해야한다.  
  
예를 들어 각 색의 이름(title) 옆에 상태로부터 해당 색을 제거하는 삭제(remove) 버튼을 덧붙이고 싶다고 하자.  
Color 컴포넌트에 이런 버튼을 추가할 수 있다.

```jsx
// Color.js
import {FaTrash} from "react-icons/fa";

export default function Color({id, title, color, rating, onRemove = f => f}){
  return (
    <section>
      <h1>{title}</h1>
      <button onClick={() => onRemove(id)}>
        <FaTrash />
      </button>
      <div style={{height: 50, backgroundColor: color}} />
      <StarRating selectedStars={rating} />
    </section>
  );
}
```

color 컴포넌트는 이벤트가 발생했다는사실과 사용자가 제거 하고 싶어하는 색에 대한 정보를 부모 컴포넌트에 전달한다.  
이렇게 이벤트와 정보를 전달하고나면 이 이벤트를 처리할 책임은 이제 부모컴포넌트의 몫이 된다.

```jsx
//ColorList.js
export default function ColorList({color = [], onRemoveColor = f => f}){
  if(!colors.length) return <div>No Colors Listed. (Add a Color)</div>;

  return (
    <div>
      colors.map(color =>(
        <Color key={color.id} {...color} onRemove={onRemoveColor} />
      ))
    </div>
  );
}
```

Color 컴포넌트의 부모는 ColorList이다. 이 컴포넌트도 상태에 접근할 수 없다. color를 제거하는 대신, ColorList도 이벤트를 부모에게 전달한다. onRemoveColor 함수 프로퍼티를 추가해서 이런 일을 수행한다. Color 컴포넌트가 onRemove 프로퍼티를 호출하면 ColorList는 자신의 onRemoveColor 프로퍼티를 호출해서 색을 제거할 책임을 자신의 부모에게 넘긴다. 이때 여전히 색의 id를 onRemoveColor 함수에게 전달할 수 있다.
  
ColorList의 부모는 App이다. 이 컴포넌트는 상태와 엮여있는 컴포넌트다. 따라서 색의 id를 사용해 상태에서 색을 제거한다.

```jsx
// App.js
export default function App(){
  const [colors, setColors] = useState(colorData);
  return (
    <ColorList
      colors={colors}
      onRemoveColor={id => {
        const newColors = colors.filter(color => color.id !== id);
        setColors(newColors);
      }}
    />
  );
}
```

먼저 setColors에 대한 변수를 추가한다.  
useState가 반환하는 배열의 두 번째 인자가 생태를 변경할 때 쓸 수 있는 함수라는 점을 기억하자.  
ColorList가 onRemoveColor 이벤트를 발생시키면 이벤트의 인자로부터 색의 id를 얻어서 색 목록에 있는 색 중에 사용자가 제거하고 싶은 색을 filter로 걸러내는 데 사용한다. 그 후 상태를 변경한다.  
setColors 함수를 사용해 사용자가 선택한 색을 제외한 색으로 이뤄진 배열로 상태를 변경한다.  
  
colors배열의 상태를 바꾸면 App 컴포넌트가 새로운 색 목록에 맞춰 다시 렌더링 된다. 이 새로운 색 목록은 ColorList 컴포넌트에 전달되며 그에 따라 ColorList 컴포넌트도 다시 렌더링 된다. ColorList는 전달받은 색에 맞춰 Color 컴포넌트를 렌더링하고 그에 따라 UI에는 색이 하나도 줄어든 새로운 화면이 그려진다.  
  
App 컴포넌트의 상태에 저장된 colors의 색 평점을 변경하려면, 방금 onRemoveColor에 대해 적용했던 방식을 그대로 onRate이벤트에 대해 적용해야 한다. 먼저 클릭된 각 별로부터 새 평점을 수집해서 StarRating의 부모에게 전달한다.

```jsx
export default function StarRating({
  totalStars= 5,
  selectedStars = 0,
  onRate = f => f
}){
  return (
    <>
      {createArray(totalStars).map((n, i) => (
        <Star 
          key={i}
          selected={selectedStars > i}
          onSelect={() => onRate(i + 1)}
        />
      ))}
    </>
  );
}
```

그 후 StarRating에 추가한 onRate 핸들러에서 평점을 얻을 수 있다.  
이제 Color 컴포넌트의 부모에게 Color 컴포넌트가 프로퍼티로 받은 다른 onRate 핸들러를 사용해서 평점을 변경할 색의 id와 평점을 전달한다.

```jsx
export default function Color(
  id,
  title,
  color,
  rating,
  onRemove = f => f,
  onRate= f => f
){
  return (
    <section>
      <h1>{title}</h1>
      <button onClick={() => onRemove(id)}>
        <FaTrash />
      </button>
      <div style={{height: 50, backgroundColor: color}} />
      <StarRating 
        selectedStars={rating} 
        onRate={rating => onRate(id, rating)}
      />
    </section>
  );
}
```

ColorList 컴포넌트는 개별 Color 컴포넌트에서 발생한 onRate 이벤트를 처리해야 한다.
이벤트를 받으면 onRateColor 함수 프로퍼티를 통해 부모에게 평점 변경 정보를 전달한다.

```jsx
export default function ColorList(
  colors = [],
  onRemoveColor = f => f,
  onRateColor = f =>f
){
  if(!colors.length) return <div>No Colors Listed. (Add a Color)</div>;

  return (
    <div className="color-lists">
      {
        colors.map(color =>(
          <Color 
            key={color.id} 
            {...color} 
            onRemove={onRemoveColor}
            onRate={onRateColor} 
          />
        ))
      }
    </div>
  );
}
```

마지막으로 모든 컴포넌트를 거처 이벤트가 위로 올라가면 App에 도착한다.
여기서 상태와 새로운 평점을 저장할 수 있다.

```jsx
// App.js
export default function App(){
  const [colors, setColors] = useState(colorData);
  return (
    <ColorList
      colors={colors}
      onRateColor={id, rating => {
        const newColors = colors.map(color =>
          color.id === id ? {...color, rating} : color
        );
        setColors(newColors);
      }}
      onRemoveColor={id => {
        const newColors = colors.filter(color => 
          color.id !== id
        );
        setColors(newColors);
      }}
    />
  );
}
```

App 컴포넌트는  ColorList가 onRateColor 프로퍼티에 새로운 평점과 색의 id를 전달해야 색 평점을 변경한다. 
onRateColor를 통해 전달 된 값을 기존 색에 매핑하면서 id 프로퍼티가 일치ㅏ는 색에 대해 새로운 평점을 할당한 배열을 구축한다.
newColors를 setColors 함수에게 전달하면 colors 상태 값이 변경되고 새로운 colors 배열 값을 가지고 App컴포넌트가 호출된다.
  
colors 배열의 상태가 바뀌면 UI 트리가 새로운 데이터에 맞춰 렌더링 된다. 새 평점은 빨간 별을 통해 사용자에게 보여진다. 프롭을 통해 데이터를 컴포넌트 트리로 내려보내는 것고 비슷하게, 사용자 상호작용은 함수 프로퍼티를 통해 데이터와 함께 트리 위로 전달한다.

## 출처
[Color Organizer React](https://github.com/enshahar/learning-react-kor/tree/seconded/chapter-06/color-organizer)