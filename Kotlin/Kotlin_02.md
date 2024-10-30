# 코틀린 핵심문법 정복하기(1)
## 1. 변수와 자료형
### 1. 변수 선언
#### 1. var, val
- var: 변경 가능한 자료형 선언
- val: 변경 불가능한 자료형 선언
**선언 키워드** 변수 이름: 자료형(DataType) = 값
```kotlin
var name:String = "Jhon"
```
### 2. 참조형 자료형
#### 1. 정수 자료형
| 자료형(부호가 없는 자료) | 크기(byte) |
| -------------- | -------- |
| Long(ULong)    | 8        |
| Int(Uint)      | 4        |
| Short(Ushort)  | 2        |
| Byte(Ubyte)    | 1        |
#### 2. 실수 자료형
| 자료형(부호가 없는 자료)  | 크기(byte) |
| --------------- | -------- |
| Double(UDouble) | 8        |
| Float(UFloat)   | 4        |
#### 3. 논리 자료형
| 자료형(부호가 없는 자료) | 크기(byte) |
| -------------- | -------- |
| Boolean        | 1        |
#### 4. 문자 자료형
| 자료형(부호가 없는 자료) | 크기(byte) |
| -------------- | -------- |
| Char           | 1        |
| String         | -        |
### 3. 표기
#### 1. 프로세스
1. ${} 사용하기
   - 변수에 내용을 표시하기 위해서 사용
2. 다중 문자열 표기
   - """ 사용 하여 줄 바꿈, 탭, 공백 문자 출력
3. 특수 문자열 표기
   - / 를 붙여 사용
### 4. 타입 체크
#### 1. 변수 체크
1. 코틀린은 변수 사용시 반드시 값이 할당되어야 함
   - null 가능성이 있는 변수는 ? 사용하여 선언
2. NPE 확인하기
   - ? 사용하기
   - !!(Non-null 단정기호) 사용하기
   - 엘비스 연산자 사용하기
### 5. 자료형 변환
#### 1. to~ 사용하기
- toByte
- toInt
- toFloat
- toLong
- toChar
- toShort
- toDouble
### 6. 자료형 검사
#### 1. is
1. 자바의 instanceOf와 동일
2. true/false 반환
```kotlin
val num = 123
	if(num is Int) {
		println("num is Int")
	}else{
		println("num is not Int")
	}
```
### 7. 자료형 캐스팅
#### 1. as
1. 묵시형을 명확한 자료형으로 지정 시 사용
2. null 가능성 as?로 사용
## 2. 연산자 활용하기
우선순위: 산술 > 비교 > 비트 > 논리
### 1. 기본 연산자
#### 1. 산술 연산자
| 연산자 | 의미  |
| --- | --- |
| +   | 덧셈  |
| -   | 뺄셈  |
| *   | 곱셈  |
| /   | 나눗셈 |
| %   | 나머지 |
#### 2. 대입 연산자
| 연산자 | 의미               |
| --- | ---------------- |
| =   | 항 대입             |
| +=  | 두 항을 더한 후 대입     |
| -=  | 두 항을 뺀 후 대입      |
| \*= | 두 항을 곱한 후 대입     |
| /=  | 두 항을 나눈 후 대입     |
| %=  | 두 항을 나머지 연산 후 대입 |
#### 3. 증가, 감소 연산자
| 연산자 | 의미      |
| --- | ------- |
| ++  | 값에 1 증가 |
| --  | 값에 1 감소 |
#### 4. 비교 연산자
| 연산자 | 의미  |
| --- | --- |
| >   |     |
| <   |     |
| >=  |     |
| <=  |     |
| ==  |     |
| !=  |     |
#### 5. 논리 연산자
| 연산자  | 의미  |
| ---- | --- |
| &&   |     |
| \|\| |     |
| !    |     |
### 2. 비트 연산자
#### 1. 비트 연산자
| 연산자  | 의미                             |
| ---- | ------------------------------ |
| shr  | Shift right(부호 비트 유지)          |
| shl  | Shift left(부호 비트 유지)           |
| ushr | Unsigned Shift right(부호 비트 이동) |
| and  | 논리 곱                           |
| or   | 논리 합                           |
| xor  | 배타적 연산                         |
| inv  | 비트를 모두 뒤집음                     |
# 2. 코틀린 핵심문법 정복하기(2)
## 1. 핵심문법 활용하기: for, while
### 반복문 사용하기
#### 1. for문
1. 시작 범위를 포함하여 범위 적용
```kotlin
for(변수 in 컬렉션 및 범위) {
	수행문
}
```
2. step을 이용하여 인덱스 증가 폭 조정
```kotlin
for(변수 in 컬렉션 및 범위 step 상수) {
	수행문
}
```
#### 2. while문
1. 조건이 맞으면 수행 코드를 수행
```kotlin
while (조건) {
	수행코드
}
```
#### 3. do while문
1. 시작 범위를 포함하여 범위 적용
```kotlin
do{
	수행코드
}while(조건)
```
### 2. 흐름 중단
#### 1. return문
1. 값을 반환할 때 사용
```kotlin
fun checkName(){
	if(name.isEmpty())
return;
	else{
		println("check")
	}
}
```
#### 2. break, continue문
1. break: for, while문에서 루프를 빠져나올 때 사용
2. continue: 수행문을 진행하지 않고 다시 반복 조건으로 돌아갈 때 사용
## 2. 핵심문법 사용하기: if, when
### 1. 조건문 사용하기
#### 1. if문
```kotlin
if(조건식){
	수행코드
}else if(조건식){
	수행코드
}else{
	수행코드
}
```
#### 2. when문
- 조건식이 길어질 때 사용
```kotlin
when(){
	조건문 -> 수행문
	조건문 -> 수행문
	else -> 수행문
}
```
## 3. 콜렉션 활용하기
### 1. 콜렉션
#### 1. 종류
1. 데이터를 모아 저장할 수 있는 자료구조
2. 불변형/가변형
3. 컬렉션 헬퍼 함수

| 불변형      | 가변형                                                       |
| -------- | --------------------------------------------------------- |
| `listOf` | `mutableListOf`, `arrayListOf`                            |
| `setOf`  | `mutableSetOf`, `hashSetOf`, `linkedSetOf`, `sortedSetOf` |
| `mapOf`  | `mutableMapOf`, `hashMapOf`, `linkedMapOf`, `sortedMapOf` |
![](../../241030_1.png)
#### 2. list
1. 순서에 따라 정렬된 요소를 가지는 컬렉션
2. 불변형: listOf(), List
3. 가변형: mutableListOf(), arrayListOf(), MutableList, ArrayList
```kotlin
var fruits = listOf("apple", "banana")
var greetings = mutableListOf("Hello", "안녕")
var animal = ArrayList<String>() //MutableListOf<String>()
greetings.add("bonjour")
println("fruits: ${fruits[0]}")
```
4. 주요함수

| 함수                                    | 설명                      |
| ------------------------------------- | ----------------------- |
| `size`                                | 리스트의 크기를 반환             |
| `get(index:Int)`                      | Index 해당하는 요소 반환        |
| `subList(fromIndex:Int, toIndex:Int)` | from에서 to 인덱스까지의 리스트 반환 |
| `add(element:E)`                      | 요소 추가                   |
| `addAll(elements:Collection\<E>)`     | 컬렉션에 포함된 모든 요소 추가       |
| `remove(element:E)`                   | 해당 요소 삭제                |
| `removeall(elements:Collection\<E>)`  | 컬렉션에 포함된 모든 요소 제거       |
| `clear()`                             | 리스트에 포함된 모든 요소 제거       |
5. `emptyList()`: 비어 있는 List를 생성해주는 헬프 함수
6. `listOfNotNull()`: 초기화 시에 null 객체를 제외한 요소만 반환하여 List를 생성해주는 헬프 함수
### 3. Set
1. 정해진 순서가 없는 요소들의 집합을 나타내는 컬렉션으로 유일성을 보장
2. 불변형: `setOf()`
3. 가변형: `mutableSetOf()`
```kotlin
val immuFruits = setOf("apple", "banana", "grape")
val muFruits = mutableSetOf("apple", "banana", "grape")
```
### 4. Map
1. 키와 값으로 구성된 컬렉션이며, 키는 중복될 수 없지만 값은 중복 가능
2. 불변형: `mapOf()`
3. 가변형: `mutableMapOf()`
```kotlin
val muMap = mutableMapOf(1 to "one", 2 to "two")
muMap.put(3, "three")
```
4. 주요 함수

| 함수                       | 설명                  |
| ------------------------ | ------------------- |
| `size`                   | Map의 크기를 반환한다       |
| `containsKey(key:K)`     | 해당 키가 존재한다면 true 반환 |
| `get(key:K)`             | 해당 값이 존재한다면 true 반환 |
| `put(key:K, value:V)`    | 해당 키에 해당하는 요소 반환    |
| `putAll(from:Map<K, V>)` | 컬렉션에 포함된 모든 요소 추가   |
| `remove(key:K)`          | 해당 키에 해당하는 요소 삭제    |
### 5. 유용한 헬프 함수
1. 특정 요소를 골라내는 함수
   - 특정 식에 따라 요소를 골라내어 새로운 리스트를 만들 때 사용
   - `filter()`, `filterNot()`, `filterKeys()`, `filterValues()`
2. 특정 범위를 가져오는 함수
   - `take()` : 범위와 해당하는 리스트를 가져오는 함수
   - `drop()` : take와 반대로 범위에 해당하는 리스트를 제외하고 가져오는 함수
3. 요소 처리와 검색
   - `binarySearch()` : 이진 탐색 후 요소의 인덱스를 반환하고 없으면 음수 값 반환
   - `find()` : 조건 식을 만족하는 첫 번째 검색된 요소를 반환하고 없으면 null 반환
