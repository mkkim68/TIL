# Generics
## Function
```ts
function getArrayLength(arr: number[] | string[] | boolean[]): number {
	return arr.length;
}
```
- 너무 복잡하고 가독성 떨어짐
```ts
function getArrayLength<T>(arr: T[]): number {
	return arr.length;
}

const array1 = [1, 2, 3];
const array2 = ["a", "b", "c"];

getArrayLength<number>(array1);
getArrayLength<string>(array2);
```
## Object
```ts
interface Vehecle<T> {
	name: string;
	color: string;
	option: T;
}

const car: Vehecle<{price: number}> = {
	name: 'Car',
	color: 'red',
	option: {
		price: 1000
	}
}

const bike: Vehicle<boolean> = {
	name: 'Bike',
	color: 'green',
	option: true
}
```
## 매개변수가 두 개라면?
```ts
const makeArr = <X, Y>(x: X, y: Y): [X, Y] => {
	return [x, y];
}

const array1 = makeArr<number, number>(4, 5);
const array2 = makeArr<string, string>("a", "b");
```
## 기본값 설정 가능
```ts
const makeArr = <X, Y=string>(x: X, y: Y): [X, Y] => {
	return [x, y];
	
const array2 = makeArr<string>("a", "b");
}
```
## extends 사용
```ts
const makeFullName = <T extends { firstName: string, lastName: string }>(obj: T) => {
	return {
		...obj,
		fullName: obj.firstName + " " + obj.lastName
	}
}

makeFullName({ firstName: "John", lastName: "Doe", location: "Seoul" })
```
## React에서 Generic
- 컴포넌트에 Props로 무엇이 올지 모르기 때문에 Generic 사용
```tsx
import React from "react";

interface Props {
	name: string;
}

const ReactComponent: React.FC<Props> = ({name}) => {
	return <div>{name}</div>
}
```
- useState도 Generic 타입 받음
```tsx
const ReactComponent: React.FC<Props> = ({name}) => {
	const [state] = useState<{name:string | null}>({name: ""});
	
	state.name
	return <div>{name}</div>;
}
```