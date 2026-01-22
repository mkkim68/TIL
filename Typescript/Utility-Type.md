# Partial
- 파셔 타입은 특정 타입의 부분 집합을 만족하는 타입을 정의할 수 있습니다.
```ts
interface Address {
	email: string;
	address: string;
}

const me: Partial<Address> = {};
const you: Partial<Address> = {email: 'john@abc.com'}; // Partial을 안쓰면 address가 없어 오류
const all: Address = {email: 'john@abc.com', address: 'john'};
```
# Pick
- 타입에서 특정 몇 개의 속성을 선택해서 타입 정의
```ts
interface Todo {
	title: string;
	description: string;
	completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

const todo: TodoPreview = {
	title: "Clean Room",
	completed: false,
}
```
# Omit
- 특정 속성만 제거해서 정의
```ts
interface Todo {
	title: string;
	description: string;
	completed: boolean;
	createdAt: number;
}

type TodoPreview = Omit<Todo, "description">;

const todo: TodoPreview = {
	title: "Clean Room",
	completed: false,
	createdAt: 12323423,
}
```
# Exclude
- 일반 Union 유형을 전달한 다음 두 번째 인수에서 제거할 멤버를 지정
```ts
type myUnionType = "1" | "2" | "3" | "4"

let lemon: myUnionType = "3"

let noLemonPlease: Exclude<myUnionType, "3"> = "1"

let noApplesOrLemons: Exclude<myUnionType, "3" | "4"> = "1"

let onlyRaspberries: Exclude<myUnionType, "3" | "4" | "2"> = "1"

let backToLemons: myUnionType = "1"
```
# Required
- 원래 유형이 일부 속성을 선택 사항으로 정의한 경우에도 객체에 Required 속성이 있는지 확인해야 하는 경우가 있음
```ts
type User = {
	firstName: string,
	lastName?: string
}

let firstUser: User = {
	firstName: "John",
}

let secondUser: Required<User> = { // 오류
	firstName: "John"
}
```
# Record <Keys, Type>
- 속성 키가 Keys이고 속성 값이 Type인 객체 type을 구성합니다.
- 이 유틸리티는 type의 속성을 다른 type에 매핑하는 데 사용할 수 있습니다.
```ts
interface CatInfo {
	age: number;
	breed: string;
}

type CatName = "miffy" | "boris" | "mordred";

const cats: Record<CatName, CatInfo> = {
	miffy: { age: 10, breed: "Persian" },
	boris: { age: 5, breed: "Maine Coon" },
	mordred: { age: 16, breed: "British Shorthair" },
}
```
# ReturnType \<T>
- 함수 T의 반환 타입으로 구성된 타입을 만듭니다.
```ts
type T0 = ReturnType<() => string>
type T1 = ReturnType<(s: string) => void>

function fn(str: string) {
	return str;
}

const a: ReturnType<typeof fn> = 'Hello';
const b: ReturnType<typeof fn> = true; // Error
```
