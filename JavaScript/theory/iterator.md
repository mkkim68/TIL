# Iterable
- 반복이 가능한 것을 Iterable하다고 함
	- `for...of`를 이용할 수 있거나
	- `[Symbol.iterator]()`이 값을 가짐
# Iterator (반복자)
- `next()`를 호출해서 `{value: , done: }` 두 개의 속성을 가지는 객체를 반환하는 객체
```js
function makeIterator(numbers) {
	let nextIndex = 0;
	
	return {
		next: function () {
			return nextIndex < numbers.length ?
				{ value: numbers[nextIndex++], done: false } :
				{ value: undefined, done: true}
		}
	}
}

const numbersArray = [1, 2, 3];

const numbersIterator = makeIterator(numbersArray);

console.log(numbersIterator.next()); // {value: 1, done: false}
console.log(numbersIterator.next()); // {value: 2, done: false}
console.log(numbersIterator.next()); // {value: 3, done: false}
console.log(numbersIterator.next()); // {value: undefined, done: true}
```
- `[Symbol.iterator]()` 이용하면 반복가능한 값을 반복기로 생성 가능
```js
const numbersIterator = numbersArray[Symbol.iterator]()
```
