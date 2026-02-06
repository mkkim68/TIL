# 문자 자료형
## 특징
- `char` - 문자 character 자료형
- 2바이트 사용 - `short`와 동일
- 유니코드상 문자
- 단따옴표를 사용하여 1개의 문자 표현 - _빈 문자 불가_
```java
// 각 문자는 상응하는 정수를 가짐  
char ch1 = 'A';  
char ch2 = 'B';  
char ch4 = 'a' + 1;  // b
char ch6 = '가' + 1;  // 각
char ch9 = '나';  

// 묵시적 형변환도 가능
int ch1Int = (int) ch1;  // 65
int ch9Int = (int) ch9;  // 45208
```
- 여러 표현 가능
```java
// 문자 리터럴과 숫자, 유니코드로 표현 가능  
char ch10 = 'A';  // A 65
char ch11 = 65;  // A 65
char ch12 = '\u0041';  // A 65
```
## 연산
### 정수와 연산
```java
char ch_a1 = 'A';  
int int_a1 = ch_a1;  
  
// 정수값을 얻는 다른 방법들 - 정수값과 연산하기  
int int_a2 = ch_a1 + 0;  
int int_a3 = ch_a1 - 0;  
  
// 리터럴에 더할 때와 변수에 더할 때 반환 자료형이 다름  
char ch_a2 = 'A' + 1;  
char ch_a3 = ch_a1 + 1; // 불가  
int int_a4 = ch_a1 + 1;
```
- `char` 자료형에는 리터럴과 정수의 연산 반환값이 들어가지 못함
### 문자로서의 숫자
```java
// 문자로서의 숫자  
char ch_b1 = '1';  
char ch_b2 = '2';  
  
// 숫자 문자에 사칙연산 - 문자 번호 기준 결과 반환  
char ch_b3 = '1' + '2';  
int int_b4 = ch_b1 + ch_b2;  
  
// 아래의 기능으로 문자가 의미하는 정수로 변환  
int int_d1 = Character.getNumericValue('1');  
int int_d2 = Character.getNumericValue('2');
int int_d3 = '5' - '0'; // 5
```
### 빈 문자 사용 불가
```java
// 빈 문자 사용 불가, 공백(Space)은 가능  
char empty = '';  // 불가
String emptyStr = "";  
  
char space = ' '; // 32
```
## 비교연산자
```java
// 같은 문자열인지  
boolean bool1 = 'A' == 'A';  
  
// 숫자와 비교할 시 해당 정수값 기준  
boolean bool2 = 'A' == 65;  
  
// 사전순 상 먼저 오는 쪽이 작음  
boolean bool3 = 'A' < 'B';
```