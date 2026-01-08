# 기본
```js
function f3(end) {
	let i = 0;
	while (i < end) {
		console.log(i);
		++i;
	}
}

f3(10); // 0 1 2 3 4 5 6 7 8 9
```
# while을 range로
```js
function f3(end) {
	_.each(console.log, L.range(end));
}

f3(10); // 0 1 2 3 4 5 6 7 8 9
```
# 효과를 each로 구분
```js
function f3(end) {
	_.go(
		L.range(end),
		_.each(console.log)
	)
}
```
- `_.each()`의 출력 결과는 들어온 인자와 동일함
	- 그렇기 때문에 **실행 중에 어떠한 효과를 일으킴**을 나타냄
