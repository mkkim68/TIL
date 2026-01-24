# 조건부 타입
```ts
type SomeType = T extends U ? X : Y
```
- T가 U에 할당 가능하면(assignable) SomeType은 X 아니면 Y
## 예제 1
```ts
type SomeType = string;
type ConditionalType = SomeType extends string ? string : null;
```
## 예제 2
```ts
function fn1<T>(value: T) {
	const fn2 = (
		arg: T extends boolean ? 'A' : 'B'
	) => {};
	return fn2;
}

const result = fn1(''); // arg: B
const result2 = fn1(true); // arg: A
```
## 예제 3
```ts
type AType<T> = T extends string | number ? T: never;
type MyResult = AType<string | number | boolean>; // here
```
- here 부분의 각각의 타입이 string | number 에 할당가능한지 체크함
- 각각의 타입을 비교하는 것을 **Distributively** 비교한다고 함
- distributively하게 비교하지 않게 하려면 함수나 튜플로 변경하면 됨
### 함수
```ts
type AType<T> = (() => T) extends () => string | number ? T: never;
type MyResult = AType<string | number | boolean>;
```
### 튜플
```ts
type AType<T> = [T] extends  [string | number]  ? T: never;
type MyResult = AType<string | number | boolean>;
```