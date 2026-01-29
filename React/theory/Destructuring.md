# 구조 분해 할당
- 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JS 표현식
- Clean Code를 위해 사용
## 객체 구조 분해 할당
```js
// 기본
function buildAnimal(animalData) {
	let accessory = animalData.accessory,
		animal = animalData.animal,
		color = animalData.color;
}

// 구조 분해 할당
function buildAnimal(animalData) {
	let {accessory, animal, color} = animalData;
}
```
## 깊게 들어간 객체 구조 분해 할당
```js
let person = {
	name: 'John',
	address: {
		zipcode: 1234,
		street: 'rainbow'
	}
}

let {address: {zipcode, street}} = person;
console.log(zipcode, street); // 1234 rainbow
```
## 배열 구조 분해 할당
```js
// 기본
const weekday = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri'];
const day1 = weekday[0];
const day2 = weekday[1];
...

// 구조 분해 할당
const [day1, day2, day3, day4, day5] = weekday;
```