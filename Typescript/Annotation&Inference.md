# Type annotation
- 개발자가 타입을 타입스크립트에게 직접 말해주는 것
```ts
const rate: number = 5;
```
# Type inference
- 타입스크립트가 알아서 타입을 추론하는 것
```ts
const rate = 5;
```
# 타입을 추론하지 못해서 타입 annotation을 꼭 해야하는 경우
## any 타입을 리턴하는 경우
```ts
const json = `{"x": 4, "y": 7}`
const coordinates = JSON.parse(json);
console.log(coordinates) // any타입
```
- coordinates의 리턴 타입이 일정하지 않으므로 any를 리턴한다고 추론함
## 변수 선언을 먼저하고 나중에 초기화하는 경우
- 변수 선언과 동시에 초기화하면 타입을 추론하지만, 선언을 먼저하고 나중에 값을 초기화할때는 추론하지 못함
```ts
let greeting
greeting = 'hello'; // any타입
```
## 변수에 대입될 값이 일정치 못하는 경우
- 여러 타입이 지정되어야 할 때에는 `|` (or statement)로 여러 타입을 애노테이션
```ts
let num = [-1, 1, 10]
let numAboveZero: boolean | number = false

for (let i = 0; i < num.length; i++) {
	if (num[i] > 0) {
		numAboveZero = num[i]
	}
}
```