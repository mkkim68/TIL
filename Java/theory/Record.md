# 레코드

- 자바 14에서 Preview로 추가, 16에서 정식 등록
- 데이터의 묶음을 저장하기 위한, 단순한 형태의 클래스

### `📁 ex01`

`☕ Gender.java`

```java
public enum Gender {
    MALE("👦🏻"), FEMALE("👧🏼");

    private String emoji;
    Gender(String emoji) { this.emoji = emoji; }
    public String getEmoji() { return emoji; }
}
```

`☕ ChildClass.java`

```java
//  기존처럼 클래스로 작성해야 했다면...
public class ChildClass {
    private final String name;
    private final int birthYear;
    private final Gender gender;

    public ChildClass(String name, int birthYear, Gender gender) {
        this.name = name;
        this.birthYear = birthYear;
        this.gender = gender;
    }

    public String getName() { return name; }
    public int getBirthYear() { return birthYear; }
    public Gender getGender() { return gender; }
}
```

`☕ Child.java`

```java
// ⭐️  레코드로 작성
public record Child(
        String name,
        int birthYear,
        Gender gender
) {}
```

`☕ Main.java`

```java
				Child child1 = new Child("홍길동", 2020, Gender.MALE);
				//  💡 toString 메소드 구현 (이후 배울 Object에서 상속받아 오버라이드)
        String childStr = child1.toString();

        Child[] children = new Child[] {
                new Child("김순이", 2021, Gender.FEMALE),
                new Child("이돌이", 2019, Gender.MALE),
                new Child("박철수", 2020, Gender.MALE),
                new Child("최영희", 2019, Gender.FEMALE),
        };

        for (Child child : children) {
            System.out.printf(
                    "%s %d년생 %s 어린이%n",
                    child.gender().getEmoji(),
                    child.birthYear(),
                    child.name()
            );
        }
```

- 레코드는 `final`
    - 다른 클래스로 상속되거나 `abstract` 로 선언 불가
- 레코드의 각 항목들은 `private`, `final`
    - 각각 같은 이름의 getter가 기본으로 만들어짐
- 인스턴스 필드를 가질 수 없음
    - 클래스 필드는 가능 _( 아래 예제에서 확인 )_

---

### 더 많은 기능들

### `📁 ex02`

`☕ InfoPrinter.java`

```java
public interface InfoPrinter {
    void printInfo ();

```

`☕ Button.java`

```java
public class Button {
    public enum ClickedBy {
        LEFT('좌'), RIGHT('우') ;
        private char indicator;
        ClickedBy(char indicator) { this.indicator = indicator; }
        public char getIndicator() { return indicator; }
    }

    //  ⭐️
    //  다른 클래스에 내부로 포함 가능
    //  인터페이스 구현 가능 (클래스 상속은 불가)
    public record ClickInfo(
            int x, int y, ClickedBy clickedBy
    ) implements InfoPrinter {

        //  💡 클래스 필드를 가질 수 있음 (인스턴스 필드는 불가)
        static String desc = "버튼 클릭 정보";

        //  💡 인스턴스/클래스 메소드를 가질 수 있음
        @Override
        public void printInfo() {
            System.out.printf(
                    "%c클릭 (%d, %d)%n",
                    clickedBy.indicator, x, y
            );
        }
    }

    public ClickInfo func (int x, int y, ClickedBy clickedBy) {
        System.out.println("버튼 동작");
        return new ClickInfo(x, y, clickedBy);
    }
}
```

`☕ Main.java`

```java
				Button button = new Button();

        Button.ClickInfo click1 = button.func(123, 456, Button.ClickedBy.LEFT);
        Button.ClickInfo click2 = button.func(492, 97, Button.ClickedBy.LEFT);
        Button.ClickInfo click3 = button.func(12, 36, Button.ClickedBy.RIGHT);

        for (Button.ClickInfo click : new Button.ClickInfo [] { click1, click2, click3 }) {
            click.printInfo();
        }
```

```java
				System.out.println("\\n- - - - -\\n");

				Button.ClickInfo click4 = button.func(111, 222, Button.ClickedBy.LEFT);
        Button.ClickInfo click5 = button.func(111, 222, Button.ClickedBy.LEFT);

				//  ⭐️  레코드 역시 참조형
        //  내용이 같은지 여부는 equals 메소드로 확인
        boolean click4n5Same = click4 == click5;
        boolean click4n5Equal = click4.equals(click5);
        boolean click4n1Equal = click4.equals(click1);
```

## **`📌 추가사항`**

- 클래스 내부에 정의된 record는 내부 정적 클래스처럼 아래와 같이 사용할 수 있습니다.