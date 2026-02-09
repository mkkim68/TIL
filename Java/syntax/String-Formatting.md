# 문자열의 포매팅과 null
## 포매팅
- 주어진 형식에 따라 문자열 생성
```java
String str1 = "%s의 둘레는 반지름 X %d X %f입니다.";  
  
String circle = "원";  
int two = 2;  
double PI = 3.14;  
  
// 13+버전
String str2 = str1.formatted(circle, two, PI);  
  
// 이전 버전
String str3 = String.format(str1, circle, two, PI);
```

| 표현  | 자료형           |
| --- | ------------- |
| %b  | 불리언           |
| %d  | 10진수 정수       |
| %f  | 실수            |
| %c  | 문자            |
| %s  | 문자열           |
| %n  | (포맷 문자열 내 바꿈) |
### printf
- 시스템의 메소드
- String.format과 같은 형식으로 출력
- 줄바꿈을 하지 않으므로 직접 넣어줘야 함
```java
System.out.printf("%s의 둘레는 반지름 X %d X %f입니다.%n", circle, two, PI);
```
#### 다양한 포매팅
- 정수
```java
String[] intFormats = {  
        "%d",           // 1. 기본  
        "%13d",         // 2. n 자리수 확보, 오른쪽 정렬  
        "%013d",        // 3. 빈 자리수 0으로 채움  
        "%+13d",        // 4. 양수는 앞에 + 붙임  
        "%,13d",        // 5. 쉼표 사용  
        "%-13d",        // 6. 자리수 확보, 왼쪽 정렬  
        "+,013d"        // 7. };
```
- 실수
```java
String[] fltFormats = {  
        "%f",           // 1. 기본 (소수점 6자리, 0으로 메움)  
        "%.2f",         // 2. 소수점 n자리 까지  
        "%13.2f",       // 3. 정수자리 확보, 소수자리 제한  
        "%,f",  
        "%+013.2f",  
        "%-13.2f"  
};  
```
- 문자열
```java
String[] strFormats = {  
        "%s",       // 1. 기본  
        "%9s",      // 2. 자리 확보  
        "%.2s",     // 3. ~글자만  
        "%9.2렬"      // 5. 왼쪽 정  
};
```
## null 문자열
- 빈 문자열과 null 다름
- null은 문자열 인스턴스 메소드 사용 불가
	- NullPointerException
- 힙에 할당되지 않음, 가리키는 곳이 없음