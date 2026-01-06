- 모든 객체는 global Object prototype을 가진다
# Prototype
- 자바스크립트 객체가 다른 객체로부터 메서드와 속성을 상속받는 매커니즘
	- 프로토타입 체인(prototype chain)
## `Object.prototype`
```js
Person.prototype.calculateAge = function() {
	// 로직
}
```
- 기존에 `Person`에 함수가 있을 때는 생성할 때마다 함수가 내부에 생성되었음
- 재사용되는 부분을 `prototype`으로 지정하면 더 효율적
## `Object.create()`
- 지정된 프로토타입 객체 및 속성을 갖는 새 객체를 만듦
```js
function Person(name, email) {
	let person = Object.create(personsPrototype);
	// 중략
	return person;
}

const personsPrototype = {
	calculateAge() {
		// 로직
	}
}
```