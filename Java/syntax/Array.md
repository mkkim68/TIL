# 배열
## 특징
- 특정 타입의 데이터를 묶음으로 다루기 위해 사용
- 지정된 자료형과 개수만큼 메모리 공간을 나란히 확보
	- [!] 개수의 변경이 불가능함
```java
char[] yutnori = {'도', '개', '걸', '윷', '모'};  
  
int length = yutnori.length;  
  
char first = yutnori[0];  
char last = yutnori[yutnori.length - 1];
```
- 사용할 자료형 뒤에 `[]` 붙여 선언
- `length`: 배열의 길이 변환
- `[]` 안에 인덱스 정수를 넣어 접근
## 초기화 및 선언
### 선언만
```java
boolean[] boolAry = new boolean[3];  // false
int[] intAry = new int[3];  // 0
double[] dblAry = new double[3];  // 0.0  
char[] chrAry = new char[3];  // 아스키 코드의 0번 글자. 문자열의 끝을 표시하는데 사용
String[] strAry = new String[3];  // null
```
- 초기화하지 않고 선언 -> 기본값 들어감
	- 원시 자료형은 기본값이 정해져 있음
	- 참조 자료형은 null
### 선언과 초기화
- 초기화 블록을 사용한 선언 동시 초기화
```java
char[] dirAry1 = {'동', '서', '남', '북'};  
char[] dirAry2 = new char[] {'동', '서', '남', '북'};  
```
- 선언만 먼저 한 상태에서는 두 번째 방법만 가능
```java
char[] dirAry3;  

dirAry3 = {'동', '서', '남', '북'};   // 불가
dirAry3 = new char[] {'동', '서', '남', '북'};
```
## 다중 배열
- 이중 배열
```java
boolean[][] dblBoolAry = new boolean[3][3];  
  
int[][] dblIntAry = new int[][] {  
        {1, 2, 3},  
        {4, 5},  
        {6, 7, 8, 9}  
};  
```
- 삼중 배열
```java
char[][][] trpChrAry = {  
        {{'자', '축'}, {'인', '묘'}},  
        {{'진', '사'}, {'오', '미'}},  
        {{'신', '유'}, {'술', '해'}}  
};
```
## 원시자료형 vs 참조자료형
- 원시 자료형은 값 자체를 복사 - 별개의 값이 됨
- 참조 자료형은 주소를 복사 - 같은 곳을 가리키게 됨
	- 문자열은 객체(참조형)지만 원시형처럼 다뤄짐
## 상수 배열
```java
final int[] NUMBERS = {1, 2, 3, 4, 5};  
  
NUMBERS = new int[] {2, 3, 4, 5, 6};  // 불가
  
NUMBERS[0] = 11;
```
- 다른 배열 할당은 불가
- 배열의 요소를 바꾸는 것은 가능
## 문자열 배열
```java
String[] strings = {"한놈", "두시기", "석삼", "너구리"};  
  
String join1 = String.join(", ", strings);
```
- `String.join(delimeter, elements)`