# userEvent
- 이전에 테스팅에서 버튼 클릭 시 `fireEvent`를 사용함
- 하지만 `userEvent`사용이 더 좋은 방법임
## userEvent란?
- fireEvent를 사용하여 만들어짐
- fireEvent를 사용하면서 엘리먼트의 타입에 따라 그 엘리먼트 타입에 맞는 더욱 적절한 반응을 보여줌
###  버튼 클릭 시
- fireEvent
	- `fireEvent.click(button)` 버튼이 focus되지 않음
- userEvent
	- `userEvent.click(button)` 버튼이 focus가 됨
- 실제 사용하는 유저가 보기에 실제 버튼을 클릭하는 행위가 더 잘 표현됨