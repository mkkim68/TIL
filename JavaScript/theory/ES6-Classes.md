- ES6 Class를 이용해 더 쉽게 OOP 구현 가능
- 문법은 OOP 방식이지만 내부에서 prototype을 사용하여 작동
```js
class Person {
	constructor(name, email, birthday) {
		this.name = name;
		// 생략
	}
	
	introduce() { // prototype에 들어감
		return `Hello I'm ${this.name}.`;
	}
}

const john = new Person('John', ...);
console.log(john.introduce()) // Hello I'm John.
```
- `constructor`: 인스턴스 생성과 동시에 클래스 필드의 생성과 초기화 실행 (생략 가능)
- `this`: 클래스가 생성할 인스턴스를 가리킴
- `new`에 의해 `constructor` 자동 호출
## Static
- 정적 메서드
- prototype이 아닌 클래스 함수 자체에 메서드 설정 가능
```js
class Person {
	constructor(name, ...) {
		this.name = name;
		// ...
	}
	
	// ...
	
	static multipleNumbers(x, y) {
		return x * y;
	}
}
```
