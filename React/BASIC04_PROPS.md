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
# 1. Memo
```jsx
function Btn({ text, changeValue }) {
  return (
	<button
	  onClick={changeValue}
	  style={{
		backgroundColor: "teal",
		color: "white",
		padding: "10px 20px",
		border: 0,
		borderRadius: 10,
	  }}
>
	  {text}
	</button>
  );
}
function App() {
  const [value, setValue] = React.useState("Save Changes");
  const changeValue = () => setValue("Revert Changes");
  return (
	<div>
	  <Btn text={value} changeValue={changeValue} />
	  <Btn text="Confirm" />
	</div>
  );
}
```
- 함수도 props에 넣을 수 있음
- 하지만 component가 많아지면 모든 component를 다시 그려줘야함
	- memo를 사용해서 component가 다시 그려질 때 우리가 컨트롤 가능함
```jsx
const MemorizedBtn = React.memo(Btn)
function App() {
  const [value, setValue] = React.useState("Save Changes");
  const changeValue = () => setValue("Revert Changes");
  return (
	<div>
	  <MemorizedBtn text={value} changeValue={changeValue} />
	  <MemorizedBtn text="Confirm" />
	</div>
  );
}
```
## 2. Prop Types
```jsx
<script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
```
- 각 prop에 입력으로 받기 원하는 type 설정 가능
	- react에서 error를 띄워 줌 
```jsx
function Btn({ text, fontSize = 14 }) {
	...
}
Btn.propTypes = {
  text: PropTypes.string.isRequired,
  fontSize: PropTypes.number,
};
```
- `PropTypes.<원하는 타입>`
- `isRequired` : 무조건 입력해야하는 prop
- `<prop이름> = <디폴트값>` : 필수가 아니어서 입력되지 않은 prop이면 디폴트값을 정해줄수 있다.
	- 입력하지 않으면 디폴트값으로 설정됨