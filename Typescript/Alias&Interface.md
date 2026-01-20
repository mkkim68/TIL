- 둘 다 타입의 이름을 지정하는 방법으로 매우 유사함
- 대부분 자유롭게 선택
# Type Alias(타입 별칭)
```ts
type People = {
	name: string
	age: number
}

const me: People = {
	name: 'John',
	age: 50
}
```
# Interface (인터페이스)
```ts
interface People {
	name: string
	age: number
}

const me: People = {
	name: 'John',
	age:  50
}
```
# 차이점
## 확장
### Interface
- `extends`
```ts
interface Animal {
	name: string;
}

interface Bear extends Animal {
	honey: boolean;
}
```
### Type
- `Intersection`
```ts
type Animal = {
	name: string;
}

type Bear = Animal & {
	honey: boolean;
}
```
## 선언 병합
### Interface
- Declaration Merging
```ts
interface Animal {
	name: string;
}

interface Animal {
	honey: boolean;
}
```
- Animal 선언 후 아래에서 다시 선언해서 병합
### Type
- 선언 병합 불가
```ts
type Animal = {       // Error
	name: string;
}

type Animal = {       // Error
	honey: boolean;
}
```
# 공통점
## Implements 사용 가능
### Interface
```ts
interface IArticle {
	category: string;
	content: string;
}

class Article implements IArticle {
	public category = '';
	public content = '';
}
```
### Type
```ts
type MyArticle = {
	category: string;
	content: string;
}

class Article implements MyArticle {
	public category = '';
	public content = '';
}
```
## Union
- 개발자가 타입 A 또는 타입 B가 될 수 있는 새 Type을 만들 수 있음
- `|` 연산자를 사용하여 Type과 Interface를 모두 사용하여 새로운 Union 유형을 생성
	- [!] 선언은 항상 type이어야 함
### Interface
```ts
interface Animal {
	name: string;
}

interface Bear {
	honey: boolean;
}

type NewType = Animal | Bear;

const bear1: NewType = {
	name: 'honey bear',
	honey: true
}
```
### Type
```ts
type Animal = {
	name: string;
}

type Bear = {
	honey: boolean;
}

type NewType = Animal | Bear;

const bear1: NewType = {
	name: 'honey bear',
	honey: true
}
```
3