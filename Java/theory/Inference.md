# 타입 추론 (Java 10+)
- Java 10에서 도입됨
- `var` 연산자로 변수 선언 - 타입을 명시하지 않음
	- 대입된 값을 통해 컴파일러가 추론
- 지역 변수에서만 사용 가능
	- 클래스의 필드로는 불가
```java
var intNum = 1;  
var doubleNum = 3.14;  
var charLet = 'A';  
var StringWord = "안녕하세요";  

// 불가
// 컴파일러가 타입을 추론할 수 없는 상황
var notInit;  
var nullVar = null;
```
- 자료형 변경 불가
- 반복문에서 편리하게 사용
- 배열의 경우 초기화시에 명시