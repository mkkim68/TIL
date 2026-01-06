# Generator Function
- 사용자의 요구에 따라 다른 시간 간격으로 여러 값 반환 가능
	- 일반 함수: 단 한 번의 실행으로 함수 끝까지 실행
	- 제너레이터 함수: 사용자의 요구에 따라 일시적으로 정지될 수도 있고 다시 시작될 수도 있음
## 생성하기
```js
function* sayNumber() { // * 꼭 붙여야 됨
	yield 1;
	yield 2;
	yield 3;
}

// 제너레이터 함수의 반환이 제너레이터
const number = sayNumbers();

console.log(number.next()); // {value: 1, done: false}
console.log(number.next()); // {value: 2, done: false}
console.log(number.next()); // {value: 3, done: false}
console.log(number.next()); // {value: undefined, done: true}
```
- `yield`는 제너레이터 함수의 실행을 일시적으로 정지시킴
	- 일반 함수의 `return`과 유사
```js
function* generatorFunction() {
	yield 1;
}

const generator = generatorFunction();
// generator는 generator[Symbol.iterator]()와 같음
```
## 사용 예시
```js
function* createIds() {
	 let index = 1;
	 
	 while(true) {
		 yield index++;
	 }
}

const gen = createIds();

// 억지로 return하는 방법도 가능
console.log(gen.return(10)); // {value: 10, done: true}
```
- **Lazy Evaluation**: 계산의 결과값이 필요할 때까지 계산을 늦춰서 필요한 데이터를 필요한 순간에 생성
```js
function* generatorFunc() {
	yield* [1, 2, 3]; // 아래와 같음
	
	// yield 1;
	// yield 2;
	// yield 3;
}
```