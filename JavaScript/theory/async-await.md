```js
async function func() {
	try {
		// 로직
	} catch (error) {
		// 에러 처리
	} finally {
		//
	}
}
```
- 비동기 코드를 마치 동기 코드처럼 보이게 함
- Promise에 then 메서드를 체인 형식으로 호출하는 것보다 가독성 좋음
- await는 async 내부 함수에서만 사용 가능
- 동기식 코드에서 쓰는 try...catch 구문을 async/await 구조에서 사용 가능