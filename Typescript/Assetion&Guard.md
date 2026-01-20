# Type Assetion(타입 단언)
- 프로그래머가 컴파일러에게 내가 너보다 타입에 더 잘 알고 있고, 나의 주장에 대해 의심하지 말라고 하는 것과 같음
- 값의 type을 설정하고 컴파일러에게 이를 유추하지 않도록 지시
```ts
var foo = {};
foo.bar = 123;
boo.bas = 'hello';

// 오류: 속성 'bar', 'bas'가 {}에 존재하지 않음
```
- type assetion을 사용해 이런 상황을 피할 수 있음
```ts
interface Foo {
	bar: number;
	bas: string;
}

var foo = {} as Foo;
foo.bar = 123;
foo.bas = 'hello';
```
# Type Guard
```ts
function func(arg: string | null) {
	return arg.toLowerCase();
}
```
- null값이 입력되면 오류가 난다.
```ts
function func(arg: string | null) {
	if (arg) { // null이 아닐 때 조건을 넣어줌으로써 guard
		return arg.toLowerCase();
	}
}
```