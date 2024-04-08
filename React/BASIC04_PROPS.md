# #0. Props
- 똑같은 요소(style과 같은)를 필요한 곳에 매번 복붙하지 않고 할 수 있는 방법이 없을까?
- 함수의 *props*를 이용
```jsx
function Btn(props) {
  return (
	<button
	  style={{
		backgroundColor: "teal",
		color: "white",
		padding: "10px 20px",
		border: 0,
		borderRadius: 10,
	  }}
>
	  {props.value}
	</button>
  );
}
function App() {
  return (
	<div>
	  <Btn value="Save Changes" />
	  <Btn value="Confirm" />
	</div>
  );
}
```
- 함수를 쓸때 `원하는 prop 이름` = `원하는 값` 으로 정해준 뒤
- 함수 내에 `{props.prop이름}` 으로 불러오면 적용됨
```jsx
function Btn({value}) {
  return (
	<button
	  style={{
		backgroundColor: "teal",
		color: "white",
		padding: "10px 20px",
		border: 0,
		borderRadius: 10,
	  }}>
	  {value}
	</button>
  );
}
```
- props가 들어가는 자리에 object를 바로 넣어주면 props.value 로 쓰지 않고 바로 value 만 불러와 접근 가능
```jsx
function Btn({ value, big }) {
  return (
	<button
	  style={{
		backgroundColor: "teal",
		color: "white",
		padding: "10px 20px",
		border: 0,
		borderRadius: 10,
		fontSize: big ? 18 : 10,
	  }}
>
	  {value}
	</button>
  );
}
function App() {
  return (
	<div>
	  <Btn value="Save Changes" big={false} />
	  <Btn value="Confirm" big={true} />
	</div>
  );
}
```
- style 속성 안에 연산을 넣어서 적용할 수도 있다