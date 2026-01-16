# Typescript Type
- 그 value가 가지고 있는 프로퍼티나 함수를 추론할 수 있는 방법
- JS에서 기본으로 제공하는 기본 제공 유형(built-in types)를 상속함
## Primitive types
| Name      | Description                             |
| --------- | --------------------------------------- |
| string    | 문자열을 나타냄                                |
| number    | 숫자 값을 나타냄                               |
| boolean   | true/false                              |
| null      | 하나의 값을 가집니다: null                       |
| undefined | 하나의 값을 가집니다: undefined 초기화되지 않은 변수의 기본값 |
| symbol    | 고유한 상수 값                                |
## Object types
| Name     | Description |
| -------- | ----------- |
| function | 함수를 나타냄     |
| array    | 배열을 나타냄     |
| classes  | 클래스를 나타냄    |
| object   | 객체를 나타냄     |
## 추가 제공 타입(from TS)
### Any
- 잘 알지 못하는 타입을 표현해야하는 경우에 사용
- 최대한 쓰지 않는게 좋음
	- `noImplicitAny`: any를 사용 시 오류가 나오게 설정 가능
### Union
- 매개변수에 대해 둘 이상의 데이터 유형을 사용 가능
```ts
let code: (string | number);
```
### Tuple
- 배열 타입을 보다 특수한 형태로 사용 가능
	- tuple에 명시적으로 지정된 형식에 따라 아이템 순서를 지정해야함
	- 추가되는 아이템 또한 tuple에 명시된 타입만 사용 가능
```ts
var employee: [number, string];

employee = [1, 'Steve'];
```
### Enum
- Enumerated Type (열거형)
- 값들의 집합을 명명하고 이를 사용할수있게 만듦
```ts
enum PrintMedia {
	Newspaper,  //0
	Newsletter, //1
	Magazine,   //2
	Book        //3
}
```
- 기억하기 어려운 숫자 대신 친숙한 이름으로 사용하기 위해 enum 사용
```ts
let LanguageCode = {
	korean: 'ko',
	english: 'en',
	japanese: 'ja',
}
```
- 언어 코드를 몰라도 사용하기 편하고 가독성이 좋아짐
#### 객체와 차이점
- object는 코드 내에서 새로운 속성을 자유롭게 추가할 수 있음
	- 속성값: 모든 타입 가능
- enum은 선언할 때 이후에 변경 불가
	- 속성값: 문자열 | 숫자
### Void
- 데이터가 없는 경우 사용됨
	- e.g. 함수가 값을 반환하지 않는 경우
```ts
function sayHi(): void {
	console.log('Hi!')
}
```
### Never
- 절대 발생하지 않을 값
	- 일반적으로 함수 리턴 타입으로 사용
```ts
function throwError(errorMsg: string): never {
	throw new Error(errorMsg);
}

function keepProcessing(): never {
	while (true) {
		console.log('')
	}
}
```
#### Void와 Never의 차이
- Void: 값으로 undefined나 null값 가질 수 있음
- Never: 어떤 값도 가질 수 없음