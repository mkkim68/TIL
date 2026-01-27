# JSX Key 속성
```jsx
{this.todoData.map((data) => (
	<div style={this.listStyle()} key={data.id}>
		<p>
			<input type="checkbox" defaultChecked={false} />
			{data.title}
			<button style={this.btnStyle}>x</button>
		</p>
	</div>
))}
```
## key 속성을 넣지 않는다면?
- 에러 발생
```
Warning: Each child in an array or iterator should have a unique "key" prop ...
```
## JSX Key 속성이란?
- 리액트에서 요소의 리스트를 나열할 때 Key를 넣어줘야 함
- React가 변경, 추가, 제거된 항목을 식별하는 데 도움이 됨
- 요소에 안정적인 ID를 부여하려면 배열 내부의 요소에 키를 제공해야 함
## key를 이용해 바뀐 부분 인식
```jsx
<ul>
	<li>1</li>
	<li>2</li>
</ul>

<ul>
	<li>3</li>
	<li>1</li>
	<li>2</li>
</ul>
```
- 이런 상황에서 key를 안 넣으면 리액트는 모든 요소를 다시 그리게 됨
- key를 넣으면 새로 추가된 3만 바뀌었다는 것을 리액트가 인식할 수 있다
## key에는 유니크한 값 사용
- index 비추천
- 배열 내부 순서에 따라 index가 바뀌기 때문