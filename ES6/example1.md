# 기본
```js
// 홀수 limit개 제곱해서 더하기
function f2(limit, list) {
	let acc = 0;
	for (const a of list) {
		if (a % 2) {
			const b = a * a;
			acc += b;
			if (--limit == 0) break;
		}
	}
	console.log(acc);
}

f2(3, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]); // 35
```
# 1. if를 filter로
```js
function f2(limit, list) {
	let acc = 0;
	for (const a of L.filter(a => a % 2, list)) {
		const b = a * a;
		acc += b;
		if (--limit == 0) break;
	}
	console.log(acc);
}

f2(3, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]); // 35
```
# 2. 값 변화 후 변수 할당을 map으로
```js
function f2(limit, list) {
	let acc = 0;
	for (const a of L.map(a => a*a, L.filter(a => a % 2, list))) {
		acc += a;
		if (--limit == 0) break;
	}
	console.log(acc);
}

f2(3, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]); // 35
```
# 3. break를 take로
```js
function f2(limit, list) {
	let acc = 0;
	for (const a of L.take(limit, L.map(a => a*a, L.filter(a => a % 2, list)))) {
		acc += a;
	}
	console.log(acc);
}

f2(3, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]); // 35
```
- `L.take(n, list)`: n개 만큼만 꺼냄
# 4. 축약 및 합산을 reduce로
```js
function f2(limit, list) {
	console.log(
		_.reduce((acc, a) => acc+a,
		0, // 초기값
		L.take(limit, 
			L.map(a => a*a, 
				L.filter(a => a % 2, list))))))
}

f2(3, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]); // 35
```
## `_.go()` 이용
```js
const add = (a, b) => a+b;

function f2(limit, list) {
	_.go(
		list,
		L.filter(a => a % 2),
		L.map(a => a*a),
		L.take(limit),
		_.reduce(add),
		console.log
	);
}

f2(3, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]); // 35
```