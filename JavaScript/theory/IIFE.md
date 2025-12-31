# IIFE(Immediately Invoked Function Expression)
- 즉시 실행 함수 표현: 정의되자마자 즉시 실행되는 JS function
```js
(
	function () {
	
	}
)()
```
- IIFE 내부에서 정의된 변수는 외부 범위에서 접근 불가
```js
var result = (function() {
	var name = "Barry";
	return name;
})();

console.log(result); // Barry
```
## 사용 목적
- 변수를 전역으로 선언하는 것을 피하기 위해
	- IIFE 내부로 다른 변수들이 접근하는 것도 막을 수 있음
- 이름 없는 함수를 위해서도 사용 가능
- 앞에 연산자를 붙여서 사용 가능
```js
+function() {return console.log("hi")}()
&(() => {return console.log("hi")})() // 화살표 함수에서는 무조건 "("로 시작
```