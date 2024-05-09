# 0. To Do List
### useState로 만든 변수에 바로 접근 불가능
- 항상 setState 함수를 사용하는데 그 안에 함수로 이전 값에 접근해서 원하는 동작을 할 수 있다.
### map을 이용해서 배열 내 요소 `li` 태그로 변환 후 출력
```js
  <ul>
	{toDos.map((item, index) => (
	  <li key={index}>{item}</li>
	))}
  </ul>
```