# Understanding State
> 버튼 클릭 횟수 출력해보기
### 어려운 방법
```jsx
const root = document.getElementById("root");
    let counter = 0;
    function countUp() {
      counter = counter + 1;
      ReactDOM.render(<Container />, root);
    }
    const Container = () => (
      <div>
        <h3>Total clicks: {counter}</h3>
        <button onClick={countUp}>Click me</button>
      </div>
    );
    ReactDOM.render(<Container />, root);
```
- 클릭할 때마다 몇 번 클릭했는지 나오게 하는 방법
	- counter에 +1 하고 변수를 element안에 담는다
	- but 렌더를 변수 값이 바뀔 때마다 해주지 않으면 초기에 렌더된 값으로 유지됨
	- 따라서 event가 일어나서 eventlistener 함수가 호출될 때마다 렌더를 해줘야함
### 간지나는 방법
```jsx
const data = React.useState(0);
const [counter, modifier] = data;
```
- `useState(초기값)` 을 하면 배열이 할당됨
- 배열의 각 idx의 값을 다시 변수에 할당하고 싶을때 저렇게 리스트에 한번에 할 수 있다!
	- \[ `데이터`, `데이터를 수정하기 위한 함수` ]
```JSX
const onClick = () => {
	modifier(counter + 1);
};
```
- event가 발생되면 (state가 바뀌면) 자동으로 요소만 리렌더링해줌
	- 화면 전체를 리렌더하는게 아님!!!
```JSX
setCounter((current) => current + 1);
```
- 똑같은 역할이지만 더 *안전함*
- react가 정확히 현재 값을 가지고 동작하게 함
# Inputs and State
### 사용자에게 input을 받아서 작동시키기
```jsx
function App() {
  const [minutes, setMinutes] = React.useState();
  const onChange = (event) => {
	setMinutes(event.target.value);
  };
  return (
	<div>
	  <h1>Super Converter</h1>
	  <label htmlFor="minutes">Minutes</label>
	  <input
		value={minutes}
		id="minutes"
		placeholder="Minutes"
		type="number"
		onChange={onChange}
	  />
	  <h4>You want to convert {minutes}</h4>
	  <label htmlFor="hours">Hours</label>
	  <input id="hours" placeholder="Hours" type="number" />
	</div>
  );
}
```
- JSX는 html과 유사하게 작성 가능하다!
	- 그러나 몇가지 attribute는 javascript 문법이므로 그대로 사용 불가능
	- `for` → `htmlFor`
	- `class` → `className`
- `useState()` 에 초기값 안넣어줘도됨
- `setState()`로 input에 입력된 값을 받아서 적용
	- input에 값이 입력된 것을 event로 알 수 있다 (input의 value로 받아옴)
	- `event.target.value`로 접근 가능
```jsx
<label htmlFor="hours">Hours</label>
<input
	value={minutes / 60}
	id="hours"
	placeholder="Hours"
	type="number"
/>
```
- hours의 input value에 `minutes/60` 변수 할당
	- 분 → 시로 변환되어 출력됨
- onChange 함수가 없기 때문에 hours의 input값을 변경해줄수는 없다
```jsx
value={Math.round(minutes / 60)}
```
- Math 함수로 반올림 가능
```jsx
// reset 버튼 생성
const reset = () => setMinutes(0);

<button onClick={reset}>Reset</button>
```
- minutes 변수와 연결된 모든 요소 리셋
```jsx
<input
	value={Math.round(minutes / 60)}
	id="hours"
	placeholder="Hours"
	type="number"
	disabled
/>
```
- disabled 속성을 이용해 hours에 input을 못 받게 해줌
#### flipped
- flip button 생성
	- `[flipped, setFlipped] = React.useState(false);`
	- `flipped`가 True면 hours -> minutes
	- False면 minutes -> hours
- 삼항 연산자를 이용하여 value를 작성해준다.
```jsx
<label htmlFor="minutes">minutes</label>
<input
	value={flipped ? amount * 60 : amount}
	id="minutes"
	placeholder="minutes"
	type="number"
	onChange={onChange}
	disabled={flipped}
/>
```
- 조건 ? 조건이 True일때 실행할 연산 : else일때 실행할 연산
- hours에도 onChange 속성 넣어주고 disabled, value에 각각 맞는 값을 넣어서 작성