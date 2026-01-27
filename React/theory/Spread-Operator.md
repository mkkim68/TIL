# 전개 연산자
- 특정 객체 또는 배열의 값을 다른 객체, 배열로 복제하거나 옮길 때 사용
- 연산자의 모양: `...` 
## 배열 조합
```js
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const arr3 = [7, 8, 9];

const arrwrap1 = arr1.concat(arr2, arr3);
const arrwrap2 = [...arr1, ...arr2, ...arr3];

console.log(arrwrap1); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
console.log(arrwrap2); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
## 객체 조합
```js
const obj1 = {
	a: 'A',
	b: 'B'
};

const obj2 = {
	c: 'C',
	d: 'D'
};

const objWrap1 = {obj1, obj2}; // 객체 자체가 들어감
console.log(objWrap1);
/*
{
	obj1: {
		a: 'A',
		b: 'B'
	},
	obj2: {
		c: 'C',
		d: 'D'
	}
}
*/

const objWrap2 = {...obj1, ...obj2}; // 각각의 값이 할당됨
console.log(objWrap2);
/*
{
	a: 'A',
	b: 'B',
	c: 'C',
	d: 'D'
}
*/
```
## 기존 배열 보존
```js
const arr1 = [1, 2, 3];
const arr2 = arr1.reverse();

console.log(arr1); // [3, 2, 1]
console.log(arr2); // [3, 2, 1]
```
- 원본 배열까지 역순으로 변경됨
```js
const arr1 = [1, 2, 3];
const arr2 = [...arr1].reverse();

console.log(arr1); // [1, 2, 3]
console.log(arr2); // [3, 2, 1]
```
- 원본 배열 유지