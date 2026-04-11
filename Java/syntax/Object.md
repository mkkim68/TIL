# 1. Object

- 모든 클래스의 조상
    
- 필드 없이 메소드들만 갖고 있음
    
    - 모든 클래스들에 상속됨
    - 필요에 따라 오버라이드하여 사용
- `Object` 인스턴스 선언하여 클래스 살펴볼 것
    
    - `@IntrinsicCandidate` : HotSpot VM _(현재 대다수 JVM)_ 에 의한 최적화
        - 작성된 코드를 보다 효율적인 내부적 동작으로 덮어씀
    - `native` : C, C++ 등 다른 언어로 작성된 코드를 호출하여 성능 향상
        - Java Natice Interface 사용

---

### `toString` 메소드

- 기본적으로는 클래스명과 해시값을 반환
- `println` 메소드로 객체 출력시 기본적으로 이 메소드의 결과값 출력
- IntelliJ 코드 생성 메뉴에서 선택

### `📁 ex01`

`☕ Button.java`

```java
public class Button {
    public enum Mode {
        LIGHT("라이트"), DARK("다크");
        Mode(String indicator) { this.indicator = indicator; }
        String indicator;
    }

    private String name;
    private Mode mode;
    private int spaces;

    public Button(String name, Mode mode, int spaces) {
        this.name = name;
        this.mode = mode;
        this.spaces = spaces;
    }

    //  ⭐️ 아래를 주석해제하고 다시 실행해 볼 것
    //  @Override
    //  public String toString() {
    //      return "%s %s버튼 (%d칸 차지)"
    //              .formatted(mode.indicator, name, spaces);
    //  }
}
```

`☕ Main.java`

```java
				Button button1 = new Button("엔터", Button.Mode.DARK, 3);

        //  💡 메소드를 ctrl/command + 클릭하여 Object 클래스 사양 살펴보기
        System.out.println(button1); // ⭐️ toString() 을 붙인 것과 같음
```

---

### `equals` 메소드

- 기본적으로는 `==` 과 같이 레퍼런스 비교
- 인스턴스 내용을 비교하려면 클래스마다 오버라이드해야 함

### `📁 ex02`

`☕ Click.java`

```java
public class Click {
    int x;
    int y;
    int timestamp;

    public Click(int x, int y, int timestamp) {
        this.x = x;
        this.y = y;
        this.timestamp = timestamp;
    }

    //  ⭐️ 아래를 주석해제하고 다시 실행해 볼 것
    //  @Override
    //  public boolean equals(Object obj) {
    //      if (!(obj instanceof Click)) return false;
    //      return this.x == ((Click) obj).x && this.y == ((Click) obj).y;
    //  }
}
```

`☕ Main.java`

```java
				Click click1 = new Click(123, 456, 5323487);
        Click click2 = new Click(123, 456, 5323487);
        Click click3 = new Click(123, 456, 2693702);
        Click click4 = new Click(234, 567, 93827345);

        boolean bool1 = click1 == click1;
        boolean bool2 = click1 == click2;
        boolean bool3 = click1 == click3;
        boolean bool4 = click1 == click4;

        boolean boolA = click1.equals(click1);
        boolean boolB = click1.equals(click2);
        boolean boolC = click1.equals(click3);
        boolean boolD = click1.equals(click4);
```

---

### `hashCode` 메소드

- 기본적으로는 각 인스턴스 고유의 메모리 위치값을 정수로 반환

### `📁 ex03`

`☕ Click.java`

```java
public class Click {
    int x;
    int y;
    int timestamp;

    public Click(int x, int y, int timestamp) {
        this.x = x;
        this.y = y;
        this.timestamp = timestamp;
    }

    //  ⭐️ 아래를 주석해제하고 다시 실행해 볼 것
    //  @Override
    //  public int hashCode() {
    //      return x * 100000 + y;
    //  }
}
```

`☕ Main.java`

```java
				Click click1 = new Click(123, 456, 5323487);
        Click click2 = new Click(123, 456, 5323487);
        Click click3 = new Click(123, 456, 2693702);
        Click click4 = new Click(234, 567, 93827345);

        int click1Hash = click1.hashCode();
        int click2Hash = click2.hashCode();
        int click3Hash = click3.hashCode();
        int click4Hash = click4.hashCode();
```

```java
				//  💡 Object의 toString은 내부에 hashCode 메소드 사용
        //  hash코드를 오버라이드하면 기본 toString에도 영향
        String click1str = click1.toString();
        String click2str = click2.toString();
        String click3str = click3.toString();
        String click4str = click4.toString();
```

```java
				String str1 = new String("Hello");
        String str2 = new String("Hello");
        String str3 = new String("World");

				boolean bool = str1 == str2;

				//  ⭐️ String 클래스 : 문자열 값이 같으면 해시값도 같도록 오버라이드 되어 있음
        int str1Hash = str1.hashCode();
        int str2Hash = str2.hashCode();
        int str3Hash = str3.hashCode();

        //  toString, equals 등도 오버라이드 되어 있음 확인
        String str1ToStr = str1.toString();
        boolean str1eq2 = str1.equals(str2);
```

---

### `clone` 메소드

- 인스턴스가 스스로를 복사하기 위해 사용
- `Cloneable` 인터페이스 구현 권장
- **깊은 복사**는 직접 오버라이드하여 구현해주어야 함

### `📁 ex04`

`☕ Click.java`

```java
public class Click {
    int x;
    int y;

    public Click(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

`☕ NotCloneable.java`

```java
public class NotCloneable {
    //  원시타입 필드들
    String title;
    int no;

    //  참조타입 필드들
    int[] numbers;
    Click click;
    Click[] clicks;

    public NotCloneable(String title, int no, int[] numbers, Click click, Click[] clicks) {
        this.title = title;
        this.no = no;
        this.numbers = numbers;
        this.click = click;
        this.clicks = clicks;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {

        //  💡 아래 super의 clone : 필드들을 얕은복사 해주는 Object 메소드
        //  - 원시타입 필드는 확실히 복사해줌. 참조타입은 참조복사만

        //  ⭐️ Cloneable을 구현하지 않은 클래스에서 호출하면 오류 발생!
        //  - 아래의 코드를 호출 안 하면 오류가 나지 않지만
        //  - 원시값 복사까지 일일이 구현해주어야 함
				//    - 즉 clone을 오버라이드해서 쓰는 의미 없음
        return super.clone();
    }
}
```

`☕ Main.java`

```java
				NotCloneable notCloneable = new NotCloneable(
                "클릭들 1", 1, new int[] {1, 2, 3},
                new Click(12, 34),
                new Click[] { new Click(12, 34), new Click(56, 78) }
        );

        NotCloneable clone1 = null;

        try { // ❓ try 문 : 오류에 대비하기 섹션에서 배울 것
             clone1 = (NotCloneable) notCloneable.clone();
        } catch (CloneNotSupportedException e) {
            System.out.printf("⚠️ 복제중 오류 발생 : %s%n", notCloneable);
        }
        //  ⚠️ 복사 실패 - CloneNotSupportedException 이라는 오류 발생
```

`☕ ShallowCopied.java`

```java
public class ShallowCopied implements Cloneable {
    String title;
    int no;

    int[] numbers;
    Click click;
    Click[] clicks;

    public ShallowCopied(String title, int no, int[] numbers, Click click, Click[] clicks) {
        this.title = title;
        this.no = no;
        this.numbers = numbers;
        this.click = click;
        this.clicks = clicks;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {

        //  Cloneable을 구현했으므로 정상 동작
        //  - 원시값만 완전히 복사됨
        return super.clone();
    }
}
```

`☕ Main.java`

```java
				ShallowCopied shallowCopied = new ShallowCopied(
                "클릭들 1", 1, new int[] {1, 2, 3},
                new Click(12, 34),
                new Click[] { new Click(12, 34), new Click(56, 78) }
        );

				ShallowCopied clone2 = null;
        try {
            clone2 = (ShallowCopied) shallowCopied.clone();
        } catch (CloneNotSupportedException e) {
            //  오류가 나지 않으므로 실행되지 않음
            System.out.printf("⚠️ 복제중 오류 발생 : %s%n", shallowCopied);
        }

        shallowCopied.title = "제목 바뀜";
        shallowCopied.no = 2;
        //  ⚠️ 참조 타입들은 완전히 복사되지 않음 (주소만 복사)
        shallowCopied.numbers[0] = 0;
        shallowCopied.click.x = 99;
        shallowCopied.clicks[0].x = 99;
```

`☕ DeepCopied.java`

```java
public class DeepCopied implements Cloneable {
    String title;
    int no;

    int[] numbers;
    Click click;
    Click[] clicks;

    public DeepCopied(String title, int no, int[] numbers, Click click, Click[] clicks) {
        this.title = title;
        this.no = no;
        this.numbers = numbers;
        this.click = click;
        this.clicks = clicks;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {

        //  원시값들 복사
        DeepCopied clone = (DeepCopied) super.clone();

        //  ⭐️ 참조타입의 복사
        //  - 원시값 요소들을 하나하나 복사해 넣음

        clone.numbers = new int[numbers.length];
        for (int i = 0; i < numbers.length; i++) {
            clone.numbers[i] = numbers[i];
        }

        clone.click = new Click(click.x, click.y);

        //  이중 참조 (인스턴스의 배열)
        //  - 이중으로 복사
        clone.clicks = new Click[clicks.length];
        for (int i = 0; i < clicks.length; i++) {
            clone.clicks[i] = new Click(clicks[i].x, clicks[i].y);
        }

        return clone;
    }
}
```

`☕ Main.java`

```java
				DeepCopied deepCopied = new DeepCopied(
                "클릭들 1", 1, new int[] {1, 2, 3},
                new Click(12, 34),
                new Click[] { new Click(12, 34), new Click(56, 78) }
        );

        DeepCopied clone3 = null;
        try {
            clone3 = (DeepCopied) deepCopied.clone();
        } catch (CloneNotSupportedException e) {
            //  오류가 나지 않으므로 실행되지 않음
            System.out.printf("⚠️ 복제중 오류 발생 : %s%n", deepCopied);
        }

        deepCopied.title = "제목 바뀜";
        deepCopied.no = 2;
        deepCopied.numbers[0] = 0;
        deepCopied.click.x = 99;
        deepCopied.clicks[0].x = 99;
```