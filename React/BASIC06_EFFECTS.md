# 0. Introduction
예를 들어 버튼을 누르면 count가 1씩 올라가는 코드를 짰다면
- 기존 useState를 사용해서 value와 setValue 함수를 사용해서 만들면 count가 올라갈때마다 페이지 전체를 다시 render를 하게 됨
- 이런 방식이 불필요한 경우가 있다.
# 1. useEffect
## `useEffect` 사용
- 코드를 언제 실행시킬지 정해줄 수 있는 함수
```js
import { useEffect } from 'react';
```
`function useEffect(effect: EffectCallback, deps?: DependencyList)`
- 두 가지의 argument를 가지는 function
	- 첫 번째 argument : 우리가 딱 한 번만 실행하고 싶은 코드 (콜백 함수)
	- 두 번째 argument : 
```js
useEffect( '함수', ?)
```
# 2. Deps
- dependency list
	- 존재하면 해당 리스트의 값이 변화할 때만 실행됨
```js
useEffect( '함수', [deps])
```
- deps 배열에 들어있는 변수가 변화할때만 함수 실행
	- 함수 내에 조건을 하나 더 넣어서 변수의 조건에 따라 함수의 실행을 결정하는 것도 가능
```js
function App() {
  const [counter, setValue] = useState(0);
  const [keyword, setKeyword] = useState("");
  const onClick = () => setValue((prev) => prev + 1);
  const onChange = (event) => setKeyword(event.target.value);

  useEffect(() => {
    console.log("I run only once");
  }, []);

  useEffect(() => {
    console.log("I run when 'keyword' changes");
  }, [keyword]);

  useEffect(() => {
    console.log("I run when 'counter' changes");
  }, [counter]);

  return (
    <div>
      <input
        value={keyword}
        onChange={onChange}
        type="text"
        placeholder="Search here..."
      />
      <h1 className={styles.title}>{counter}</h1>
      <button onClick={onClick}>Click me</button>
    </div>
  );
}
```
- react가 우리에게 준 선물 
	- 어떤 변수가 변하는 지에 따라 각각 다른 동작을 할 수 있다!!!
# 4. Cleanup
- useEffect를 사용할 떄 요소가 생성됐을 때, 변화했을 때 특정 함수를 실행시킬 수 있었음
	- 특정 요소가 destroy될때도 가능하다!!
```javascript
import { useState, useEffect } from "react";

function Hello() {
  useEffect(() => {
    console.log("created :)"); // 요소가 생성되었을 때
    return () => console.log("destroyed :("); // 요소가 파괴되었을 때
  }, []);
  return <h1>Hello</h1>;
}

function App() {
  const [showing, setShowing] = useState(false);
  const onClick = () => setShowing((prev) => !prev);
  return (
    <div>
      {showing ? <Hello /> : null}
      <button onClick={onClick}>{showing ? "Hide" : "Show"}</button>
    </div>
  );
}
```
- useEffect 내에서 실행할 함수 내에서 return `특정 함수` 를 하면 요소가 붕괴될 때 실행
- 위의 예시처럼 `useEffect` 내에 모든 함수를 작성한다 (일반적으 함수를 따로 분리하여 정의해서 사용하지 않는다고 함)