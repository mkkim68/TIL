# Understanding State
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