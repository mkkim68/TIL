# this란
- 현재 실행 중인 코드에서 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수
- this가 가리키는 값(this의 바인딩)은 함수 호출 방식에 의해 동적으로 결정됨
## this의 바인딩
### 일반 함수 호출
- 기본적으로 전역 객체가 바인딩됨
- 브라우저에서 `window`, Node.js에서 `global`
- strict 모드에서는 `undefined`
```js
function foo() {
	console.log(this)	
}

foo() // window
```
- 함수가 호출될 때 this가 결정됨
### 화살표 함수 호출
- this가 존재하지 않음
- 함수가 정의된 위치에 따라 **외부 스코프의 this를 캡쳐**해서 사용
#### 선언식 함수 사용
```js
const person = {
	name: 'Seo',
	sayName: function() {
		innerFun = function() {
			return `안녕하세요 ${this.name}님`
		}
		console.log(innerFun()) // 안녕하세요 ''님
	}
}

person.sayName()
```
- 일반 함수 호출되었기 때문에 this는 `window`
#### 화살표 함수 사용
```js
const person = {
	name: 'Seo',
	sayName: function() {
		innerFun = () => {
			return `안녕하세요 ${this.name}님` // 안녕하세요 Seo님
		}
		console.log(innerFun())
	}
}

person.sayName()
```
- 일반 함수로 호출되었으나 innerFun이 화살표 함수로 선언이 되어 있어 상위 스코프에서 this가 person이 됨
### 메서드 호출
- this는 해당 메서드가 속한 객체
```js
const person = {
	name: 'Seo',
	sayName() {
		console.log(this.name)
	}
}

person.sayName()  // Seo
```
### apply, bind, call 메서드에 의한 간접 호출
#### call 메서드
- 함수를 실행하고 함수의 첫번째 인자로 전달하는 값에 바인딩
```js
function getUser(a, b, c) {
	console.log(this.name)
	console.log(this.gender)
	console.log(a+b+c)
}

const person = {
	name: 'Seo',
	gender: 'Female'
}

getUser.call(person, 1, 2, 3)
// Seo
// Female
// 6
```
#### apply 메서드
- call과 함수 인수 전달 방식만 다를 뿐, 동일하게 동작함
- 호출할 함수의 인수를 배열로 묶어 전달
```js
function getUser(a, b, c) {
	console.log(this.name)
	console.log(this.gender)
	console.log(a+b+c)
}

const person = {
	name: 'Seo',
	gender: 'Female'
}

const numbers = [1, 2, 3]

getUser.apply(person, numbers)
// Seo
// Female
// 6
```
#### bind 메서드
- 사용한 함수와 똑같이 생긴 함수를 반환함
- bind 메서드를 이용하면 함수를 호출해야함
```js
function getUser(a, b, c) {
	console.log(this.name)
	console.log(this.gender)
	console.log(a+b+c)
}

const person = {
	name: 'Seo',
	gender: 'Female'
}

console.log(getUser.bind(person, 1, 2, 3))
// f getUser 함수가 그대로 콘솔에 출력

getUser.bind(person, 1, 2, 3)()
// Seo
// Female
// 6
```
### new 생성자 내부에서의 this
- this는 새로운 객체를 참조함
- new 키워드로 생성자 함수를 호출 시, this는 새로 생성된 객체를 가리킴
```js
class Circle(radius) {
	constructor(radius) {
		this.radius = radius;
	}
	
	getDiameter() {
		return 2 * this.radius;
	}
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1)
// Circle {radius: 5, getDiameter: function()}

console.log(circle1.getDiameter()) // 10
console.log(circle2.getDiameter()) // 20
```