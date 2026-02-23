# 클래스 기초
## 클래스/객체 없이 프로그래밍을 한다면?
```java
		//  1 버튼
        char btn1Print = '1';
        int btn1Space = 1;
        String btn1Mode = "DARK";
        placeButton(btn1Print, btn1Space, btn1Mode);

        //  더하기 버튼
        char btnPlusPrint = '+';
        int btnPlusSpace = 3;
        String btnPlusMode = "DARK";
        placeButton(btnPlusPrint, btnPlusSpace, btnPlusMode);

        //  클리어 버튼
        char btnClearPrint = 'C';
        int btnClearSpace = 2;
        String btnClearMode = "DARK";
        placeButton(btnClearPrint, btnClearSpace, btnClearMode);
```
- 같은/유사한 형식의 반복되는 코드들
- 보다 반복을 줄이고, 체계적이고 안정적이게 이 버튼들을 다룰 방법 필요
## 클래스 & 인스턴스
- `YalcoChicken.java`
```java
//  본사의 코드
public class YalcoChicken {
    //  인스턴스가 가질 필드(field)들
    int no;
    String name;

    //  인스턴스가 가질 메소드 - 💡 static을 붙이지 않음
    String intro () {
        // no와 name 앞에 this를 붙인 것과 같음
        return "안녕하세요, %d호 %s점입니다."
                .formatted(no, name);
    }
}
```
- Main.java와 같은 위치에 생성
- 클래스: 각 버튼이 갖고 있을 속성(들)과 기능(들)을 정의
- - `Main.java`
```java
		//  본사 소속의 매장을 내는 코드
		YalcoChicken store1 = new YalcoChicken();
        store1.no = 3; // 🔴
        store1.name = "판교";

        YalcoChicken store2 = new YalcoChicken();
        store2.no = 17;
        store2.name = "강남";


        //  인스턴스의 필드들에 접근
        int store1No = store1.no;
        String store2Name = store2.name;

        //  인스턴스의 메소드 호출
        String store1Intro = store1.intro();
```
- 객체 _object_ / 인스턴스 _instance_ : 속성(프로퍼티)들과 기능(메소드)들의 묶음
    - 자바에서는 객체와 인스턴스를 같은 것으로 이해해도 됨
- 인스턴스는 클래스에서 정의한 방식으로 양산됨
## 생성자 메소드
- `YalcoChicken.java`
```java
public class YalcoChicken {
    int no;
    String name;

    //  ⭐ 생성자(constructor) : 인스턴스를 만드는 메소드
		//  ⭐ this : 생성될 인스턴스를 가리킴
    public YalcoChicken (int no, String name) {
        this.no = no;
        this.name = name;
    }

    String intro () {
				//  String name = "몽고반"; // 주석해제 시 name 대체
        return "안녕하세요, %d호 %s점입니다." // 🔴
                .formatted(no, name);
    }
}
```
- `Main.java`
```java
		//  클래스로 인스턴스를 생성 - 💡 new 연산자 + 생성자 호출
        //  본사의 방침대로 매장을 내는 것
        YalcoChicken store1 = new YalcoChicken(3, "판교");
        YalcoChicken store2 = new YalcoChicken(17, "강남");
        YalcoChicken store3 = new YalcoChicken(24, "제주");

        String[] intros = {store1.intro(), store2.intro(), store3.intro()};
```
- 메서드 이름 없이, 반환 타입(해당 클래스) 뒤로 괄호가 따라옴
- `return`을 명시하지 않음 - 해당 클래스 타입의 인스턴스 반환
- `new` 연산자와 함께 사용되어 인스턴스를 반환
- 필수 작성 아님 - 언제나 같은 내용의 인스턴스를 반환할 경우
    - 작성되지 않았을 경우에는 인자 없이 호출 (이전 예제 확인)
    - ⭐️ 코드에 작성하지 않아도 컴파일러가 자동 생성
        - `.class` 파일에서 확인 가능
- 자동생성
    - 메뉴 - 코드 - 생성
        - 윈도우: `alt` + `insert`
        - 맥: `command` + `N`
    - `생성자` 선택
    - `name` 과 `price` 선택
- 💡 생성자를 작성하지 않는다고 생성자가 없는 것이 아님
### ⭐️ `this` - 만들어질 인스턴스를 가리킴
- `intro` 메소드 브레이크포인트에서 `this` 항목 확인
    - `no` 와 `name` 에 `this` 를 붙인 것과 같음
- 메소드 내에서 같은 이름의 변수나 인자가 없다면 식별자는 `this` 의 필드를 가리킴
- 같은 이름의 변수나 인자가 있다면 덮어씌워짐
    - 필드에는 `this`를 붙여 구분
### 클래스의 인스턴스도 참조 자료형
- 배열과 같이, 인스턴스도 필드로 들어간 데이터들을 포함하는 주머니
- 메소드에 인자로 들어갈 시, 인스턴스의 **주소값**이 복사되어 들어감
    - 복사된 주소지만 같은 주머니를 가리키므로…