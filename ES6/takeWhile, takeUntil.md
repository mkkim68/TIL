# takeWhile
```js
_.go(
	[1, 2, 3, 4, 5, 6, 7, 8, 0, 0, 0],
	_.takeWhile(a => a),
	_.each(console.log)); // 1 2 3 4 5 6 7 8
)
```
- `takeWhile` true일 때 까지만 담는다
# takeUntil
```js
_.go(
	[1, 2, 3, 4, 5, 6, 7, 8, 0, 0, 0],
	_.takeUntil(a => !a),
	_.each(console.log)); // 1 2 3 4 5 6 7 8 0
)
```
- `takeUntil` 처음 true를 만나는 지점까지만 담는다