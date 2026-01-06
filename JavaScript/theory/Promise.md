# Promise
- 자바스크립트 비동기 처리에 사용되는 객체
- 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타냄
```js
const myPromise = new Promise((resolve, reject) => {
	// 비동기 작업
	
	// resolve(someValue) // fulfilled
	// or
	// reject("failure reason") // rejected
});
```
- 매개변수로 "실행 함수"를 받음
	- `resolve`: 비동기 작업을 성공적으로 완료해 결과를 값으로 반환할 때 호출
	- `reject`: 작업이 실패하여 오류의 원인을 반환할 때 호출하면 됨
- 이행이나 거부될 때, 프로미스의 `then` 메서드에 의해 대기열(큐)에 추가된 처리기들이 호출됨
```js
myPromise
	.then((result) => { // resolve
	
	})
	.catch((err) => { // reject
	
	})
	.finally(() => { // 어떤 상태든 모두 여기로
	
	})
```
## `Promise.all()`
- 순회 가능한 객체에 주어진 모든 프로미스가 이행한 후, 혹은 프로미스가 주어지지 않았을 때 이행하는 Promise 반환
- 주어진 프로미스 중 하나가 거부하는 경우
	- 첫 번째로 거절한 프로미스의 이유를 이용해 자신도 거부
```js
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
	setTimeout(resolve, 3000, 'foo');
});

Promise.all([promise1, promise2, promise3]).then((values) => {
	console.log(values);
});

// Array [3, 42, "foo"]
```
## `Promise.race()`
- Promise 객체 반환
- 이 프로미스 객체는 iterable 안에 있는 프로미스 중 가장 먼저 완료된 것의 결과값으로 그대로 이행되거나 거부됨
```js
const promise1 = new Promise((resolve, reject) => {
	setTimeout(resolve, 500, 'one');
})

const promise2 = new Promise((resolve, reject) => {
	setTimeout(resolve, 100, 'two');
})

Promise.race([promise1, promise2]).then((value) => {
	console.log(value);
})

// "two"
```
