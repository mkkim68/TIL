# 자료형과 변수
## 자료형
```java

// 참/거짓 - boolean        
System.out.println(true);  
System.out.println(false);  

// 숫자  
System.out.println(123); // int  
System.out.println(3.14); // double  

// 문자 - char        
System.out.println('A');  
System.out.println('가');  
System.out.println('⭐');  

// 문자열 - String        
System.out.println("동네형보다 많은 자료형");  

```
## 변수
- ⭐ 자바는 정적 자료형
- [!] 변수에 설정한 자료형과 자료형이 다른 데이터는 넣을 수 없음
- 크기가 다른 자료형으로 변경할 수 없음
- 컴파일 단계에서 차단됨
### 식별자 명명 규칙
- 문자, 숫자, 언더스코어, 달러사인 포함 가능
	- 한글도 사용은 가능 - 권장 X
- 문자 또는 `$`, `_`로 시작해야 함
- 공백을 포함할 수 없음
```java
int mk, _mk, $mk, 민경; // 가능

// 불가
int 1mk;
int min kyoung;
int #mk;
```
### 식별자 명명 관례
- 클래스는 대문자로 시작
- 상수는 대문자와 `_` 사용
	- `PI`
- 변수나 메서드는 camelCase 사용
	- `myName`
### 예약어 (reserved words)
- 식별자로 사용 불가능한 키워드들
```java
// 사용 불가
int double;
boolean instanceof;
char new;
```
## 한 번에 여러 개 선언, 초기화
```java
char ch1, ch2, ch3;
char ch4 = 'A', ch5 = 'B', ch6 = 'C';
```
## 변수의 값을 다른 변수에 넣기
```java
int numA = 1;
int numB = numA; // 1
```
- [I] 원시 타입 데이터는 값을 복사해서 줌
## 주의
- 같은 변수를 두 번 선언 불가
- 선언 후 초기화하기 전 사용 불가
## 상수
```java
final int INT_NUM = 1;
INT_NUM = 2; // 불가능
```
- 선언, 초기화 후 값 변경 불가