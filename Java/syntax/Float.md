# 실수 자료형들
```java
double a = 0.1, b = 0.2;  
  
double c = a + b;  // c: 0.30...04
  
boolean bool = 0.1 + 0.2 == 0.3; // false
```

| 자료형    | 크기    |
| ------ | ----- |
| float  | 4byte |
| double | 8byte |
## double
- double: float보다 단순히 범위가 넓은 것이 아니라 보다 정밀하게 표현 가능
```java
// float의 최대값과 최소값  
float fMin = -Float.MAX_VALUE;  
float fMax = Float.MAX_VALUE;  
  
// double의 최대값과 최소값  
double dMin = -Double.MAX_VALUE;  
double dMax = Double.MAX_VALUE;  
  
// 최소 절대값  
float fAbsMin = Float.MIN_VALUE;  
double dAbsMin = Double.MIN_VALUE;  
  
// ⭐ double이 범위도 넓고, 정밀도도 높음 확인  
boolean bool1 = Float.MAX_VALUE < Double.MAX_VALUE;  
boolean bool2 = Float.MIN_VALUE > Double.MIN_VALUE;

// 최대 정밀도 테스트
double dblNum = 0.123456789123456789;  // 0.12345678912345678
float fltNum = 0.123456789123456789f;  // 0.12345679
```
## float
- 뒤에 f 또는 F를 붙여 표현
```java
float flt1 = 3.14f;  
double dbl1 = 3.14;  

// float에는 double을 담을 수 없음
float flt2 = dbl1;  
// 반대는 가능
double dbl2 = flt1;
```
- 명시적 형변환을 해야 함
```java
float flt2 = (float) dbl1;  
```
## 특징
### 정수 대입
- 묵시적 변환
- [I] float(4byte)에도 long(8byte)의 값 담을 수 있음
```java
long lng1 = 123;  

float flt3 = lng1;  // 123.0
double dbl3 = lng1;  // 123.0
```
- ⭐ 큰 수(정확히 표현 가능한 한도를 넘어서는)일 경우
	- 가능한 최대 정확도로
```java
long lng2 = Long.MAX_VALUE;  

float flt4 = lng2;  
double dbl4 = lng2;
```
### 대입 연산
```java
float fl5 = 123.45f;  
fl5 += 6.78;  // 130.23
fl5++;  // 130.23
fl5++;  // 131.23
fl5--;  // 132.23
// 131.23
```
### 이항 연산
```java
float flt01 = 4.124f;  
float flt02 = 4.125f;  
double dbl01 = 3.5;  
  
// float끼리의 연산은 float 반환  
float flt03 = flt01 + flt02;  
  
// float과 double의 연산은 double 반환  
float flt04 = flt01 + dbl01; // 불가
```
#### 오차
```java
// 부동소수점 방식상 오차 자주 있음  
double dbl02 = 0.2 + 0.3f;  
double dbl03 = 0.2f * 0.7f;  
double dbl04 = 0.4 - 0.3;  
double dbl05 = 0.9f / 0.3;  
double dbl06 = 0.9 % 0.6;  
  
// 소수부가 2의 거듭제곱인 숫자간 연산은 오차 없음  
double dbl07 = 0.25 * 0.5f;  
double dbl08 = 0.5 + 0.25 + 0.125 + 0.0625;
```
- [I] 부동소수점 오차 해결을 위해서는 이후 배울 `BigDecimal` 클래스 사용
### 정수 자료형과 연산
```java
int int1 = 5;  
float flt1 = 2f;  
double dbl1 = 3;  
double dbl2 = 7;  
  
// 정수 자료형과 실수 자료형의 계산은 실수 반환
int fit2 = int1 / flt1;  // 불가
double dbl3 = int1 / dbl1;  
double dbl4 = dbl2 / int1;  
  
// 리터럴로 작성시 double임을 명시하려면 .0을 붙여줄 것
double dbl5 = 5 / 2;  // 2
double dbl6 = 5.0 / 2;  
double dbl7 = (double) 5 / 2;
```
#### 정수로 변환
- 정수 자료형에 강제로 넣으면 소수부 버림
### 비교 연산
- 정수/실수 간, 다른 숫자 자료형 간 사용 가능