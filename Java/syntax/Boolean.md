# 불리언 자료형과 관련 연산자
## 특징
- `boolean` 자료형
- 참/거짓 둘 중 하나 가짐
- 1바이트 (8비트) 공간 차지
	- 하드웨어 구조와의 호환성 - CPU가 수월히 다룰 수 있는 최소 단위
- 리터럴보다는 반환값으로 많이 사용됨
```java
boolean bool1 = true;  
boolean bool2 = false;
```
## 연산
### 부정 연산자
```java
boolean bool3 = !true;  
boolean bool4 = !false;  
  
boolean bool5 = !!bool3;  
boolean bool6 = !!!bool3;
```
### 논리 연산자
| syntax   | meaning |
| -------- | ------- |
| a && b   | and    |
| a \|\| b | or      |
- [I] &&가 || 보다 우선순위 높음
### 단축평가 (short circuit)
- `&&`: 앞의 것이 `false`면 뒤의 것을 평가할 필요 없음
- `||`: 앞의 것이 `true`면 뒤의 것을 평가할 필요 없음
- 평가는 곧 실행 - 이 점을 이용한 간결한 코드
- [I] 연산 부하가 적은 코드를 앞에 - 리소스 절약
#### 부수 효과가 있는 경우라면?
```java
int a = 1, b = 2, c = 0, d = 0, e = 0, f = 0;  
  
boolean bool1 = a < b && c++ < (d += 3);  // c: 1, d: 3 boo1: true
boolean bool2 = a < b || e++ < (f += 3);  // e: 0, f: 0 boo2: true
```
- `bool2`의 경우엔 앞이 `true`라 뒤의 연산을 실행하지 않음
### 삼항 연산자
```
a ? b : c
```
- a: 불리언 값
- b: a가 true일 때 반환될 값
- c: a가 false일 때 반환할 값
```java
int num1 = 3, num2 = 4;  
  
char num1OE = num1 % 2 == 1 ? '홀' : '짝';  // 홀
char num2OE = num2 % 2 == 1 ? '홀' : '짝';  // 짝
```
#### 다중으로 사용 가능
```java
int num = 3;  
boolean mult2 = true;  
boolean plus5 = true;  
  
System.out.println(  
        (!mult2 && !plus5) ? num  
                : (mult2 && plus5) ? num * 2 + 5  
                : mult2 ? num * 2  
                : num + 5  
);
```
#### 단축 평가 적용됨
```java
int x=1, y=2;  
  
int changed1 = x < y ? (x += 2) : (y += 2); // x: 3, y: 2
```
