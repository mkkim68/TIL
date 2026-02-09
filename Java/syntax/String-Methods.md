# 문자열의 메소드들
## 특징
- 문자열은 불변 immutable
- 문자열 스스로를 변경하는 메소드는 없음
	- 새 문자열 또는 다른 값을 반환
	- [!] 문자열 변수에 다른 값을 넣을 수 없다는 뜻이 아님
## 메소드
### 길이 반환
```java
int int1 = "".length()
```
### 빈 문자열 여부
```java
String str1 = "";  
String str2 = " \t\n";  
  
boolean bool1 = str1.isEmpty();  // true
boolean bool2 = str2.isEmpty();  // false
  
boolean bool3 = str1.isBlank();  // true
boolean bool4 = str2.isBlank();  // true
```
- `isEmpty()` : 문자열의 길이가 0인지 여부
- `isBlank()`: 공백(white space)를 제외한 문자열의 길이가 0인지 여부
### 트리밍
```java
String str3 = "\t abc \n";  
String str4 = str3.trim();  // str4: "abc"
```
- 앞 뒤 공백 제거
#### 변수 그 자체에 적용
```java
str3 = str3.trim();
```
- 문자열은 불변: 변수가 가리키는 참조값 변경
### 문자 반환
```java
char ch1 = str1.charAt(0);
```
### 문자(열) 위치 반환
```java
int int1 = str2.indexOf("a")
int int2 = str2.indexOf("a", 4);
```
- `indexOf, lastIndexOf(ch/str, [fromIndex])`: fromIndex부터 일치하는 첫/마지막 문자(열)의 위치
- 포함되지 않는 문자는 -1 반환
### 값 동일 여부
```java
boolean bool1 = str1.equals(str2);
boolean bool2 = str1.equalsIgnoreCase(str2);
```
- `equals`: 대소문자 구분하여 비교
- `equalsIgnoreCase` : 대소문자 구분하지 않고 비교
### 포함 여부 확인
```java
boolean bool1 = str1.contains("hi");
boolean bool2 = str1.startsWith("hi");
boolean bool3 = str1.endsWith("hi");
```
-  `contains`: 포함 여부
- `startsWith(prefix, [toffset])`: (주어진 위치에서) 해당 문자열로 시작 여부
- `endsWith`: 해당 문자열로 끝남 여부
### 정규표현식 일치 여부 확인
```java
boolean bool1 = str1.matches(emailRegex);
```
- `matches()`
- [정규표현식](https://ko.wikipedia.org/wiki/정규_표현식)
### 문자열 비교
- `compareTo()`
- 같은 문자열이면 0 반환
```java
String str_a1 = "ABC";  
String str_a2 = "ABCDE";  
String str_a3 = "ABCDEFG";  

int int_a1 = str_a1.compareTo(str_a1);  
```
- 시작하는 부분이 같을 때는 글자 길이의 차이 반환
```java
int int_a2 = str_a1.compareTo(str_a2);  // -2
int int_a3 = str_a2.compareTo(str_a1);  // 2
```
- 시작하는 부분이 다를 때는 첫 글자의 정수값 차이 반환
```java
String str_a4 = "HIJKLMN";  
  
int int_a4 = str_a1.compareTo(str_a4);  // -7
int int_a5 = str_a4.compareTo(str_a1);  // 7
```
- `compareToIgnoreCase()` : 대소문자 구분 없이 비교 
```java
String str_b1 = "abc";  
String str_b2 = "DEF";  
  
int int_b1 = str_b1.compareTo(str_b2);  // 29
int int_b2 = str_b1.compareToIgnoreCase(str_b2);  // -3
```
### 대소문자 변환
- `toUpperCase()`
- `toLowerCase()`
### 이어붙이기
```java
String str3 = str1.concat(str2)
```
#### + 연산자와의 차이
1. concat에는 문자열만 이어붙일 수 있음
2. 필요시에만 새 인스턴스 생성
3. null이 포함될 경우
	- + 연산자는 null과 이어붙이기 가능
	- `concat`은 **NullPointerException** 발생
4. 다중 연산시 생성되는 문자열 인스턴스의 수가 다름
	```java
	  
    String str1 = "a" + "b" + "c" + "d";  
  
    String str2 = new StringBuilder("a")  
            .append("b")  
            .append("c")  
            .append("d")  
            .toString(); // "abcd" 생성됨  
    // "a", "b", "c", "d", "abcd"가 생성되어 메모리 차지  
  
    String str3 = "a"  
            .concat("b")  // "ab" 생성  
            .concat("c")  // "abc" 생성  
            .concat("d") // "abcd" 생성  
    // "a", "b", "c", "d", "ab", "abc" "abcd"가 생성되어 메모리 차지
	```
- + 연산: 다중 연산시 메모리 절약
	- 반복 연산에는 무의미
	- 반복 연산시 명시적으로 `StringBuilder`, `StringBuffer` 등 사용
- 성능이 중요한 상황이 아니라면 상황에 따라 메서드 체이닝 등의 편의를 위해 `concat` 사용
### 반복하기
```java
String a2 = a1.repeat(2);
```
- `repeat(count)`: count만큼 반복
### 잘라오기
```java
String b2 = b1.substring(7);
String b3 = b1.substring(7, 10);
```
- `substring(beginIndex, [endIndex])`: ~번쨰 문자부터 (~번쨰 문자까지) 잘라서 반환
### 치환
```java
String c2 = c1.replace("보쌈", "중국")
```
- `replace(target, replacement)`: target을 replacement로 바꿈
	- 여럿 포함시 모두 치환
	- 원본은 바뀌지 않음
	- 문자도 가능
- ⭐정규표현식 사용 가능
	- `replaceAll`: 전부 치환
	- `replaceFirst`: 첫 번쨰 일치부분만 치환
### 배열 반환
- `toCharArray()`: 문자 배열로
- `split(regex, [limit])`: regex 기준으로 (~개 까지) 분할하여 문자열 배열로 반환