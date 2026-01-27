# React State
- 컴포넌트의 렌더링 결과물에 영향을 주는 데이터를 갖고 있는 객체
	- State가 변경되면 컴포넌트는 리렌더링 됨
	- State는 컴포넌트 안에서 관리됨
- **데이터가 변할 때 화면을 다시 렌더링 해주기 위해 사용**
```jsx
state = {
	todoData: [
		{
			id: "1",
			title: "todo 1",
			completed: true,
		},
		{
			id: "2",
			title: "todo 2",
			completed: false,
		},
	]
}

this.state.todoData
const newTodoData = []
this.setState({todoData: newTodoData})
```
