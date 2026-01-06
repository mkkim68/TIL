# Symbol이란
- 2015년 ES6에서 새로 추가된 원시 타입
- 유니크한 식별자를 만들기 위해서 사용됨
## 생성 방법
| Type   | 생성          | Shortcut    | 결과        |
| ------ | ----------- | ----------- | --------- |
| String | String("5") | "5"         | "5"       |
| Number | Number(5)   | 5           | 5         |
| Symbol | Symbol("5") | Symbol("5") | Symbol(5) |
## 목적
- 유니크한 식별자를 위해 사용
- 보이는 건 같아도 내부에선 다른 값을 가짐
```js
const sym1 = Symbol();
const sym2 = Symbol();

console.log(sym1 === sym2); // false
```
## description
- 해당 심볼에 대한 설명으로 식별을 쉽게 하기 위함
```js
const sym3 = Symbol('hi');
console.log(sym3.description); // hi
```
## 특징
### `for...in`과 `getOwnPropertyNames()`에서 제외됨
- 심볼을 이용하면 기본적으로 Property가 숨겨짐 (찾을 수 있는 방법 있음)
- `for...in`과 `getOwnPropertyNames`를 이용하면 Symbol로 만든 프로퍼티는 안보임
### `getOwnPropertySymbols()` 이용
- 해당 메서드를 사용해야 심볼 프로퍼티 볼 수 있음
## `Symbol.for()`을 이용한 전역 심볼
- 원래는 심볼로 값 생성시 심볼의 description이 같더라도 다 다른 값을 가짐
- `Symbol.for()`을 이용하면 같은 description을 가졌을 때 같은 값을 가짐
```js
Symbol('id') === Symbol('id') // false
Symbol.for('id') === Symbol.for('id') // true
```
## `Symbol.keyFor()`
- `Symbol.for()`를 이용해서 전역 심볼을 만들 때 사용하는 description을 얻을 수 있음
```js
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

alert(Symbol.keyFor(sym)); // name
alert(Symbol.keyFor(sym2)); // id
```