# 얕은 복사(Shallow Copy)
- 중첩된 배열이나 객체가 있다면 얕은 복사 후 그 중첩된 부분을 변경시 모두 바뀜

- spread operator
- `Object.assign()`
- `Array.from()`
- `slice`
## 얕은 동결
- `Object.freeze()`
	- 객체를 동결함 -> 더 이상 변경 불가
- 깊은 부분은 동결 안됨
# 깊은 복사(Deep Copy)
- `JSON.parse(JSON.stringify())`
- nested spread operator
```javascript
const aObj = {
	"a": "a",
	"b": "b",
	"cObj": { "a": 1, "b": 2 }
}

const newObj = {...aObj, cObj: {...aObj.cObj}}
```
- lodash 라이브러리를 이용한 deepCopy