# 열거형
### 지정된 선택지 내의 값을 받을 변수 사용시

```java
		//  문자열로 설정: 불안정함
        String mode = "LIGHT";
        mode = "DARK";
        
        mode = "lite"; // 실수를 간편히 방지할 방법이 없음
```

```java
		//  1: LIGHT, 2: DARK
		//  위 정보를 숙지해야 함 - 가독성 현저히 떨어짐
        int mode = 1;
        mode = 2;
        
		//  타 변수에 사용되는 값들과 구분되지 않음
		//  잘못된 범위의 값 입력에 대응하기 번거로움
        int spaces = 3;
        
        mode = spaces; // 이러한 실수를 방지하기 어려움
```

---

### `📁 ex01`

`☕ [ButtonMode.java](<http://ButtonMode.java>)` - 새 파일 생성시 `enum` 으로

```java
public enum ButtonMode {
    LIGHT, DARK
}
```

`☕ ButtonSpace.java`

```java
public enum ButtonSpace {
    SINGLE, DOUBLE, TRIPLE
}
```

`☕ Button.java`

```java
public class Button {
    private ButtonMode buttonMode = ButtonMode.LIGHT;
    private ButtonSpace buttonSpace = ButtonSpace.SINGLE;

    public void setButtonMode(ButtonMode buttonMode) {
        this.buttonMode = buttonMode;
    }

    public void setButtonSpace(ButtonSpace buttonSpace) {
        this.buttonSpace = buttonSpace;
    }
}
```

`☕ Main.java`

```java
				Button button1 = new Button();

        button1.setButtonMode(ButtonMode.DARK);
        button1.setButtonSpace(ButtonSpace.TRIPLE);

        //  ⚠️ 아래와 같은 오용이 방지됨
        button1.setButtonMode(ButtonSpace.DOUBLE);
```

---

### 클래스 내부에 작성하여 오용 여지 제거하기

- 버튼에 사용되는 속성들이므로…

### `📁 ex02`

`☕ Button.java`

```java
public class Button {
    enum Mode { LIGHT, DARK }
    enum Space { SINGLE, DOUBLE, TRIPLE }

    private Mode mode = Mode.LIGHT;
    private Space space = Space.SINGLE;

    public void setMode(Mode mode) {
        this.mode = mode;
    }

    public void setSpace(Space space) {
        this.space = space;
    }
}
```

`☕ Main.java`

```java
				Button button1 = new Button();

        button1.setMode(Button.Mode.DARK);
        button1.setSpace(Button.Space.DOUBLE);
```

---

### enum의 추가 기능들

- 클래스처럼 필드, 생성자, 메소드를 가질 수 있음

### `📁 ex03`

`☕ YalcoChickenMenu.java`

```java
public enum YalcoChickenMenu {
    FR("후라이드", 10000, 0),
    YN("양념치킨", 12000, 1),
    GJ("간장치킨", 12000, 0),
    RS("로제치킨", 14000, 0),
    PP("땡초치킨", 13000, 2),
    XX("폭렬치킨", 13000, 3);

    private String name;
    private int price;
    private int spicyLevel;

    YalcoChickenMenu(String name, int price, int spicyLevel) {
        this.name = name;
        this.price = price;
        this.spicyLevel = spicyLevel;
    }

    public String getName() { return name; }
    public int getPrice() { return price; }

		public void setPrice(int price) {
        this.price = price;
    }

    public String getDesc () {
        String peppers = "";
        if (spicyLevel > 0) {
            peppers = "🌶️".repeat(spicyLevel);
        }

        return "%s %s원 %s"
                .formatted(name, price, peppers);
    }
}
```

`☕ Main.java`

```java
				YalcoChickenMenu menu1 = YalcoChickenMenu.YN;
        YalcoChickenMenu menu2 = YalcoChickenMenu.RS;
        YalcoChickenMenu menu3 = YalcoChickenMenu.XX;

				
				// ⛑️ 이번 챕터부터 영상에서 var로 표시했던
        // 자료형을 명시적으로 수정합니다.
				String menu1Name = menu1.getName();
        int menu2Price = menu2.getPrice();
        String menu3Desc = menu3.getDesc();
```

```java
				menu2.setPrice(16000);
        int menu2NewPrice = menu2.getPrice();
```

```java
				//  ⭐️ 열거형의 메소드들

        YalcoChickenMenu[] byNames = new YalcoChickenMenu[] {
                YalcoChickenMenu.valueOf("FR"),
                YalcoChickenMenu.valueOf("PP"),
                YalcoChickenMenu.valueOf("GJ"),
                //  YalcoChickenMenu.valueOf("NN"), // ⚠️ 런다임 에러
        };

        //  💡 name 메소드 : 각 항목의 이름 반환
        String[] names = new String[] {
                menu1.name(), menu2.name(), menu3.name()
        };

        //  💡 ordinal 메소드 : 순번 반환
        int[] orders = new int[] {
                menu1.ordinal(), menu2.ordinal(), menu3.ordinal()
        };

        //  💡 values 메소드 : 전체 포함된 배열 반환
        //  YalcoChickenMenu[] 자료형
        YalcoChickenMenu[] menus = YalcoChickenMenu.values();

        for (YalcoChickenMenu menu : menus) {
            System.out.println(menu.getDesc());
        }
```

`☕ YalcoChicken.java`

```java
public class YalcoChicken {
    static YalcoChickenMenu[] menus = YalcoChickenMenu.values();

    public void takeOrder (String menuName) {
        YalcoChickenMenu ordered = null;

        for (YalcoChickenMenu menu : menus) {
            if (menu.getName().equals(menuName)) {
                ordered = menu;
            }
        }

        if (ordered == null) {
            System.out.println("해당 메뉴가 없습니다.");
            return;
        }

        System.out.println(
                ordered.getPrice() + "원입니다."
        );
    }
}
```

`☕ Main.java`

```java
				System.out.println("\\n- - - - -\\n");

        YalcoChicken store1 = new YalcoChicken();

        for (String menuName : "양념치킨,능이백숙,땡초치킨".split(",")) {
            store1.takeOrder(menuName);
        }
```
