# 커링 (Currying)
- 함수와 함께 사용하는 고급기술
- 다른 언어에도 존재

- `f(a,b,c)`처럼 단일 호출로 처리하는 함수를 `f(a)(b)(c)`와 같이 각각의 인수가 호출 가능한 프로세스로 호출된 후 병합될 수 있게 변환하는 것
```js
const sum = (x, y) => x + y;
const curriedSum = x => y => x+y;

console.log(curriedSum(10)); // y => x+y
console.log(curriedSum(10)(20)); // 30
```
## parameter 갯수 상관 없이 사용
```js
function curry(func) {
	return function curried(...args) {
		if (args.length >= func.length) {
			return func.apply(this, args);
		} else {
			return function (...args2) {
				return curried.apply(this, args.concat(args2));
			}
		}
	}
}

const sum = (x, y, z, j) => x+y+z+j;
const curriedSum = curry(sum);
console.log(curriedSum(1)(2)(3)(4)); // 10 
```
