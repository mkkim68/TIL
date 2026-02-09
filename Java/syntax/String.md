# 문자열 자료형과 기초 사용법
- [methods](./String-Methods.md)
- [formatting](./String-Formatting.md)
## 특징
- `String` : 문자열 자료형
- 0~다수의 문자들로 구성
- 쌍따옴표로 둘러쌈
- 이제까지 배운 자료형들과 달리 **참조 자료형**
	- 그러나 특별히 원시값과 유사하게 사용될 수 있음
```java
// 리터럴 방식  
String st1 = "Hello World!";  
String st2 = "안녕하세요✋ 반갑습니다~";  
  
// 빈 문자열 가능  
String str3 = "";  
  
// 인스턴스 생성 방식  
String str4 = new String("나중에 자세히 배웁니다.");
```
## 값 비교
```java
String hl1 = "Hello";  
String hl2 = "Hello";  
String wld = "World";  
  
// 리터럴끼리는 == 을 사용하여 비교 가능  
boolean bool1 = hl1 == hl2;  // true
boolean bool2 = hl1 == wld;  // false
```
- 인스턴스 비교는 다름
```java
String hl3 = new String("Hello");  
String hl4 = new String("Hello");  
  
// 인스턴스와 비교 시 .equals 메소드 사용해야 함
// 특별한 경우가 아니라면 메소드로 비교
boolean bool3 = hl3 == hl4;  // false  
boolean bool4 = hl1.equals(hl2);  
boolean bool5 = hl3.equals(hl4);
```
- 같은 곳을 참조하는 인스턴스
	- 메소드 사용 없이 비교해도 참조값이 같으므로 true 반환
```java
String hl5 = hl4;  

boolean bool6 = hl4 == hl5; // true
```
#### 비교 대상/생성 위치
- 비교하는 대상이 다름
	- `==` : 참조값 비교 (메모리 위치)
	- `.equals()`: 내용 비교
- 생성 위치가 다름
	- 리터럴로 생성 시 **String constant pool**이란 곳에 중복 없이 저장됨
		- 같은 문자열이 적힌 리터럴 변수들은 같은 것을 가리킴
	- 객체 인스턴스로 생성 시 매 번 새로 생성되어 각각 자리를 차지
- 메모리상 주소 식별자 비교
```java
// 아래 2개 동일
int hl1hash = System.identityHashCode(hl1);  
int hl2hash = System.identityHashCode(hl2);  

// 다른 주소
int hl3hash = System.identityHashCode(hl3);  

// 아래 2개동일
int hl4hash = System.identityHashCode(hl4);  
int hl5hash = System.identityHashCode(hl5);
```
## 연산자
### equals
```java
boolean b1 = "안녕".equals("안녕");
```
- 리터럴로 바로 비교 가능
### + 연산자
```java
String s1 = "Hello, ";  
String s2 = "World!";  
  
String s3 = s1 + s2; // Hello, World!
```
### += 연산자
- 해당 변수에 문자열 이어붙임 (부수효과)
```java
String c1 = "안녕. ";  
c1 += "친구들"; // 안녕. 친구들

String c2 = c1 += "나는 바보야."; // c1, c2: 안녕. 친구들 나는 바보야.
```
- `+=` 연산자만 사용 가능
### 다른 자료형과 연산
- 단순히 텍스트로 바꿔서 쭉 이어붙이게 됨
## 형변환
### 다른 자료형에서 문자열로
- 메소드 이용
```java
String str1 = String.valueOf(true); // "true"
```
- 단순한 방법
```java
String str2 = true + ""; // "true"
```
### 문자열에서 다른 자료형으로
```java
String str123 = "123";  
  
byte bytNum = Byte.parseByte(str123);  
short srtNum = Short.parseShort(str123);  
int intNum = Integer.parseInt(str123);  
long lngNum = Long.parseLong(str123);
```
 - Wrapper class에 있는 parse 메소드 사용
 ```java
boolean b1 = Boolean.parseBoolean("TRUE");  // true
boolean b2 = Boolean.parseBoolean("true");  // true
boolean b3 = Boolean.parseBoolean("T");  // false
 ```
 - Boolean은 대소문자 무관 'true' 일때만 true 반환
 ```java
 char chr = strA.charAt(0);
 ```
 - 0번째 문자를 char로 반환
#### 범위를 넘어가면
```java
byte bNum = Byte.parseByte("12345");  
int iNum = Integer.parseInt("123.45");  
double dNum = Double.parseDouble("하나");
```
- 자료형에 맞지 않거나 범위를 넘어가면 **런타임 에러**
## 이스케이프 표(Escape Sequence)
| 이스케이프 표현 | 대체      |
| -------- | ------- |
| `\"`     | 큰따옴표    |
| `\'`     | 작은따옴표   |
| `\n`     | 줄바꿈     |
| `\t`     | 탭       |
| `\\`     | 백슬래시 하나 |
