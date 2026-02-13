# 메소드
## 특징
- 타 언어의 함수와 같은 개념
- 자바는 모든 것이 클래스의 요소이므로 메소드라 부름
### 의미
#### 1. 반복을 최소화
```java  
public class Ex01 {  
    static void main(String[] args) {  
  
        double xx = 3, yy = 4;  
        addSubtMultDiv(xx, yy);  
  
        xx = 10; yy = 2;  
        addSubtMultDiv(xx, yy);  
  
        xx = 7; yy = 5;  
        addSubtMultDiv(xx, yy);  
    }  
  
    //  ⭐️ 메인 메소드 외부에 선언할 것  
    static void addSubtMultDiv (double a, double b) {  
        System.out.printf("%f + %f = %f%n", a, b, a + b);  
        System.out.printf("%f - %f = %f%n", a, b, a - b);  
        System.out.printf("%f * %f = %f%n", a, b, a * b);  
        System.out.printf("%f / %f = %f%n", a, b, a / b);  
    }  
}
```
#### 2. 값을 받고 연산하여 결과값을 반환
```java
static int add (int num1, int num2) {
	return num1 + num2;
}
```
- 반환 = 바꿔 쓸 수 있다
- 메서드 실행문을 메서드 반환값으로 치환
![](https://yalco.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fba681e29-01d9-4b92-b0e1-0563d466d5ef%2F%25E1%2584%2583%25E1%2585%25A2%25E1%2584%258C%25E1%2585%25B5_9_%25E1%2584%2589%25E1%2585%25A1%25E1%2584%2587%25E1%2585%25A9%25E1%2586%25AB.png?table=block&id=20fa01f4-cbe8-45d0-99ef-1a6e631c4f4d&spaceId=f5787b06-7575-49c2-8c2c-d197061c3d0f&width=1280&userId=&cache=v2)
- `static` : 정적 메소드 _(클래스 메소드)_ 에서 호출하려면(main 등) 붙어야 함
    - 정적이 아닌 메소드 _(인스턴스 메소드)_ 는 객체지향 섹션에서 배울 것
- **매개변수** _parameter_ : 각각 자료형과 변수명을 적음. 없을 시 빈 괄호
    - 호출할 때 넣는 값 (`add(3, 4)` 의 3과 4)을 **인자 _argument_** 라고 함
    - 강의에서는 자주 인자라고 통일하여 부를 것
- `return` : 반환하는 값이 있을 때, **맨 마지막에** 붙임
### 다양한 용례
```java
static int count = 0;  
  
//  매개변수 없이 값만 반환하는 메소드  
//  외부 변수 값을 변화시킴 (static이므로 static 변수만 가능)  
static int getCount () {  
    System.out.println("카운트 증가");  
    return ++count;  
}
```
- `return` 을 `println` 윗줄로 옮겨 볼 것
    - `return` 은 블록을 종료하므로 이후의 코드 무효화 - 컴파일 에러 발생
- 반환값의 자료형을 바꿔 볼 것 *(`short`, `long`, 기타…)
    - 반환값이나 인자의 자료형에 어긋날 경우 컴파일 에러 발생
- ⚠️ 외부의 변수 값을 바꾸는 것은 좋은 메서드가 아님
```java
	//  자바의 메소드는 하나의 값만 반환 가능
    //  여러 값을 반환하려면 배열 또는 이후 배울 객체를 활용
    static int[] getMaxAndMin (int[] nums) {

        int max = nums[0];
        int min = nums[0];
        for (int num : nums) {
            max = max > num ? max : num;
            min = min < num ? min : num;
        }

        return new int[] {max, min};
		}
```
### 매개변수의 개수가 정해지지 않은 메소드
```java
	//  💡 ... 연산자 : 해당 위치 뒤로 오는 연산자들을 배열로 묶음
    //  int[] (배열 자체를 받음)과는 다름!
    static double getAverage(int... nums) {
        double result = 0.0;
        for (int num : nums) {
            result += num;
        }
        return result / nums.length;
    }
```
- 배열을 넣으면 자동으로 펼쳐져 인식됨
```java
        int[] numbers = {3, 91, 14, 27, 4};
        double avgOfArr = getAverage(numbers);
```
- 다른 (정해진) 인자들과 사용시 맨 마지막에
```java
    static String descClass (int classNo, String teacher, String... kids) {
        return "%d반의 담임은 %s 선생님, 원생들은 %s 입니다."
                .formatted(classNo, teacher, String.join(", ", kids));
    }
```
## 메소드 오버로딩
- 같은 메소드 이름, 다른 매개변수
- 다른 자료형의 값들로 같은 성질의 작업을 정의할 때
```java
	static int add(int a, int b) { return a + b; }

    //  매개변수의 개수가 다름
    static int add(int a, int b, int c) { return a + b + c; }

    //  매개변수의 자료형이 다름
    static double add(double a, double b) { return a + b; }

    //  매개변수의 자료형 순서가 다름
    static String add(String a, char b) { return a + b; }
    static String add(char a, String b) { return a + b; }

    //  ⚠️ 반환 자료형이 다른 것은 오버로딩 안 됨 - 다른 함수명 사용
    static double add(int a, int b) { return (double) (a + b); }
```
### 원시형 매개변수 vs 참조형 매개변수
```java
	//  ⭐️ 원시값은 '복사해서' 가져옴
    //  메소드 내부에서 값을 변경해도 원본에 영향 끼치지 않음
    static void modifyIntArg (int num) {
        System.out.printf("수정 전: %d%n", num++);
        System.out.printf("수정 후: %d%n", num);
    }

    //  ⭐️ 참조값은 주소값이므로 원본 그 자체를 가리킴
    static  void modifyAryElem (int[] ary) {
        System.out.printf("수정 전: %d%n", ary[1]++);
        System.out.printf("수정 후: %d%n", ary[1]);
    }
```
### 재귀 메소드
- 스스로를 호출하는 메소드
- 호출시마다 메모리에 스택이 축적 - 초과시 스택오버플로우 _stack overflow_ 에러
```java
	static void upTo5 (int start) {
        System.out.println(start);
        if (start < 5) {
            upTo5(++start);
        } else {
            System.out.println("-- 종료 --");
        }
    }
```
- 다른 메소드를 호출한 메소드는 호출된 메소드가 종료될 때까지 메모리에 남아 있음
    - 호출이 반복될수록 위와 같이 메소드들이 쌓이게 됨
#### 꼬리 재귀 최적화
- 재귀 코드를 내부적으로 루프 형태로 바꿔서 스택이 쌓이지 않도록 함
- [!] 자바에서는 현재 기본적으로 제공하지 않음 (보안 등 문제…)
- 반복 횟수가 너무 많아지는 작업에는 사용하지 말 것!