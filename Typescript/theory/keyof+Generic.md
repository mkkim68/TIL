- Typescript의 keyof 연산자는 주어진 객체 Type에서 속성 이름의 Union Type을 얻는 데 사용됩니다.
- 이를 통해 객체의 키를 수동으로 나열하지 않고도 객체의 키를 나타내는 Type을 정의할 수 있습니다.
- keyof를 사용하면 특정 속성 이름을 미리 알지 않고도 객체의 속성에 의존하는 유형을 정의할 수 있음.
- 이를 통해 광범위한 객체 및 속성과 함께 작동할 수 있는 보다 일반적인 코드를 작성할 수 있으므로 코드의 재사용성과 적응성 더욱 높아짐
## 함수 생성하기
```ts
interface Person {
	name: string;
	age: number;
	address: string;
}

const person: Person = {
	name: "John",
	age: 30,
	address: "Seoul",
};

const age = getProperty(person, 'age'); // 30
const name = getProperty(person, 'name'); // John
const invalid = getProperty(person, 'invalid') // Error

function getProperty<T, K extends keyof T>(obj: T, key: K) {
	return obj[key];
}
```