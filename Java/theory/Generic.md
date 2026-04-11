# 3. 제네릭

- 자료형을 필요에 따라 동적으로 정할 수 있도록 해 줌
    - 자료형을 변수로 갖는다고 이해
- 메소드 또는 클래스에 사용

### 제네릭 메소드

### `📁 ex01`

`☕ Main.java`

```java
		//  제네릭 메소드
		//  T : 타입변수. 원하는 어떤 이름으로든 명명 가능
		public static <T> T pickRandom (T a, T b) {
        return Math.random() > 0.5 ? a : b;
    }
```

```java
		int randNum = pickRandom(123, 456);
        boolean randBool = pickRandom(true, false);
        String randStr = pickRandom("마루치", "아라치");

				//  import sec05.chap08.ex01.YalcoChicken;
        YalcoChicken store1 = new YalcoChicken("판교");
        YalcoChicken store2 = new YalcoChicken("역삼");
        YalcoChicken randStore = pickRandom(store1, store2);

        //  ⚠️ 타입이 일관되지 않고 묵시적 변환 불가하면 오류
        //  double randFlt = pickRandom("hello", "world");
        double randDbl = pickRandom(12, 34);
```

```java
		public static <T> void arraySwap (T[] array, int a, int b) {
        if (array.length <= Math.max(a, b)) return;
        T temp = array[a];
        array[a] = array[b];
        array[b] = temp;
    }
```

```java
				//  원시값 배열(double[])을 쓰면 오류 - 배열로는 오토박싱이 안 되므로
        Double[] array1 = new Double[] {
                1.2, 2.3, 3.4, 4.5, 5.6, 6.7, 7.8
        };
        Character[] array2 = new Character[] {
                'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K'
        };

        arraySwap(array1, 3, 5);
        arraySwap(array2, 2, 7);
```

```java
				// 셔플
        for (int i = 0; i < 100; i++) {
            arraySwap(
                    array2,
                    (int) Math.floor(Math.random() * array2.length),
                    (int) Math.floor(Math.random() * array2.length)
            );
        }
```

---

### 제네릭 클래스

### `📁 ex02`

`☕ Pocket.java`

```java
//  원하는 자료형들로 세 개의 필드를 갖는 클래스
public class Pocket<T1, T2, T3> {
    private T1 fieldA;
    private T2 fieldB;
    private T3 fieldC;

    public Pocket(T1 fieldA, T2 fieldB, T3 fieldC) {
        this.fieldA = fieldA;
        this.fieldB = fieldB;
        this.fieldC = fieldC;
    }

    public T1 getFieldA() {
        return fieldA;
    }

    public T2 getFieldB() {
        return fieldB;
    }

    public T3 getFieldC() {
        return fieldC;
    }
}
```

`☕ Main.java`

```java
				//  선언시 아래와 같이 자료형에 각 타입변수의 자료형을 명시
        //  - 제내릭에는 원시값이 아닌 클래스만 사용 가능
				//  - (래퍼 클래스의 또 다른 존재 이유)
        Pocket<Double, Double, Double> size3d1 =
                new Pocket<>(123.45, 234.56, 345.67);

        //  타입추론도 가능은 함
        var size3d2 =
                new Pocket<>(123.45, 234.56, 345.67);

        double width = size3d1.getFieldA();
        double height = size3d1.getFieldB();
        double depth = size3d1.getFieldC();

        Pocket<String, Integer, Boolean> person =
                new Pocket<>("홍길동", 20, false);

        //  제네릭 클래스는 배열 생성시 new로 초기화 필수
        Pocket<String, Integer, Boolean>[] people = new Pocket[] {
                new Pocket<>("홍길동", 20, false),
                new Pocket<>("전우치", 30, true),
                new Pocket<>("임꺽정", 27, true),
        };
```

---

### **`📌 추가사항`** 생성시 오른쪽에 빈 `<>` 을 붙이는 이유

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f5787b06-7575-49c2-8c2c-d197061c3d0f/6e2f6dc1-14af-4ab2-959e-cb1a233dca7f/Untitled.png)

빈 `<>` 라도 붙이지 않으면 생성하는 인스턴스의 자료형을 체크하지 않습니다. 때문에 자료형에 맞게 대입해도 컴파일러가 걸러내지 못하죠. `<>` 를 붙이면 타입추론을 통해 자료형에 맞는 제네릭을 채워 넣게 되고, 그렇게 함으로써 의도한 바에 맞지 않은 자료형을 사용했을 때 컴파일 오류를 발생시켜 예상치 못한 문제를 차단하게 됩니다.

위의 코드에서 첫줄은 제네릭 타입을 잘못 사용했음에도 불구하고 오류가 나지 않지만 두번째 줄은 컴파일 오류가 발생하는 것을 볼 수 있습니다. 때문에 두번째 줄의 코드는 개발자가 코드를 잘못 작성했음을 사전에 알고 수정할 수 있습니다.

---

### 제한된 제네릭

### `📁 ex03`

`☕ Main.java`

```java
		//  💡 T는 Number를 상속한 클래스이어야 한다는 조건
    public static <T extends Number> double add2Num(T a, T b) {
        return a.doubleValue() + b.doubleValue();
    }
    //  ❓ 그냥 Number를 인자 자료형으로 하면 되지 않을까?
```

```java
				double sum1 = add2Num(12, 34.56);
        double sum2 = add2Num("1" + true); // ⚠️ 불가
```

```java
		//  ⭐ 상속받는 클래스와 구현하는 인터페이스(들)을 함께 조건으로
    //  여기서는 클래스와 인터페이스 모두 extends 뒤에 &로 나열
    public static <T extends Mamal & Hunter & Swimmer>
    void descHuntingMamal (T animal)  {
        //  ⭐️ 조건에 해당하는 필드와 메소드 사용 가능
        System.out.printf("겨울잠 %s%n", animal.hibernation ? "잠" : "자지 않음");
        animal.hunt();
    }

    public static <T extends Flyer & Hunter>
    void descFlyingHunter (T animal) {
        animal.fly();
        animal.hunt();
    }
```

```java
				descHuntingMamal(new PolarBear());
        descHuntingMamal(new GlidingLizard()); // ⚠️ 불가

        descFlyingHunter(new Eagle());
        descFlyingHunter(new GlidingLizard());
        descFlyingHunter(new PolarBear()); // ⚠️ 불가
```

---

### `📁 ex04`

`☕ FormElement.java`

```java
public abstract class FormElement {
    public enum MODE { LIGHT, DARK }

    private static MODE mode = MODE.LIGHT;

    public void printMode () {
        System.out.println(mode);
    }

    abstract void func ();
}
```

`☕ Clickable.java`

```java
public interface Clickable {
    void onClick();
}
```

`☕ Button.java`

```java
public class Button extends FormElement implements Clickable {
    @Override
    public void onClick() { func(); }

    @Override
    void func() { System.out.println("버튼 클릭");}
}
```

`☕ Switch.java`

```java
public class Switch extends FormElement implements Clickable {
    private boolean isOn;

    public Switch(boolean isOn) {
        this.isOn = isOn;
    }

    @Override
    public void onClick() { func(); }

    @Override
    void func() {
        isOn = !isOn;
        System.out.printf("%s(으)로 전환%n", isOn ? "ON" : "OFF");
    }
}
```

`☕ TextInput.java`

```java
public class TextInput extends FormElement {
    @Override
    void func() {
        System.out.println("텍스트 입력 받음");
    }
}
```

`☕ HyperLink.java`

```java
public class HyperLink implements Clickable {
    @Override
    public void onClick() {
        System.out.println("링크로 이동");
    }
}
```

`☕ FormClicker.java`

```java
public class FormClicker<T extends FormElement & Clickable> {
    private T formElem;

    public FormClicker(T formElem) {
        this.formElem = formElem;
    }

    //  ⭐️ 조건의 클래스와 인터페이스의 기능 사용 가능
    //  - 자료형의 범위를 특정해주므로
    public void printElemMode () {
        formElem.printMode();
    }

    public void clickElem () {
        formElem.onClick(); // 이 부분이 Clickable의 메소드
    }
}
```

`☕ Main.java`

```java
				FormClicker<Button> fc1 = new FormClicker<>(new Button());
        FormClicker<Switch> fc2 = new FormClicker<>(new Switch(true));

        fc1.printElemMode();
        fc2.clickElem();

        //  ⚠️ 조건에 부합하지 않는 클래스 사용 불가
        FormClicker<TextInput> fc3 = new FormClicker<>(new TextInput());
        FormClicker<HyperLink> fc4 = new FormClicker<>(new HyperLink());
```

---

### 와일드카드

- 제네릭 클래스에 대한 다형성을 위함

### `📁 ex05`

`☕ Unit.java`

```java
public class Unit {}
```

`☕ Knight.java`

```java
public class Knight extends Unit {}
```

`☕ MagicKnight.java`

```java
public class MagicKnight extends Knight {}
```

`☕ Horse.java`

```java
public class Horse<T extends Unit> {
    private T rider;

    public void setRider(T rider) {
        this.rider = rider;
    }
}
```

`☕ Main.java`

```java
				//  아무 유닛이나 태우는 말
        Horse<Unit> avante = new Horse<>(); // ⭐️ Horse<Unit>에서 Unit 생략
        avante.setRider(new Unit());
        avante.setRider(new Knight());
        avante.setRider(new MagicKnight());

        //  기사 계급 이상을 태우는 말
        Horse<Knight> sonata = new Horse<>(); // Knight 생략
        sonata.setRider(new Unit()); // ⚠️ 불가
        sonata.setRider(new Knight());
        sonata.setRider(new MagicKnight());

        //  마법기사만 태우는 말
        Horse<MagicKnight> grandeur = new Horse<>();
        grandeur.setRider(new Unit()); // ⚠️ 불가
        grandeur.setRider(new Knight()); // ⚠️ 불가
        grandeur.setRider(new MagicKnight());
```

```java
				//  ⚠️ 자료형과 제네릭 타입이 일치하지 않으면 대입 불가
        //  - 제네릭 타입이 상속관계에 있어도 마찬가지
        Horse<Unit> wrongHorse1 = new Horse<Knight>();
        Horse<Knight> wrongHorse2 = new Horse<Unit>();
        avante = sonata;
        sonata = grandeur;
```

```java
				//  ⭐️ 와일드카드 - 제네릭 타입의 다형성을 위함

        //  💡 Knight과 그 자식 클래스만 받을 수 있음
        //  기사 계급 이상을 태우는 말 이상만 대입할 받을 수 있는 변수
        Horse<? extends Knight> knightHorse;
        knightHorse = new Horse<Unit>(); // ⚠️ 불가
        knightHorse = new Horse<Knight>();
        knightHorse = new Horse<MagicKnight>();
        knightHorse = avante; // ⚠️ 불가
        knightHorse = sonata;
        knightHorse = grandeur;
```

```java
				//  💡 Knight과 그 조상 클래스만 받을 수 있음
        //  마법기사만 태우는 말은 받지 않는 변수
        Horse <? super Knight> nonLuxuryHorse;
        nonLuxuryHorse = avante;
        nonLuxuryHorse = sonata;
        nonLuxuryHorse = grandeur; // 불가
```

```java
				//  💡 제한 없음 - <? extends Object>와 동일
        //  어떤 말이든 받는 변수
        Horse<?> anyHorse;
        anyHorse = avante;
        anyHorse = sonata;
        anyHorse = grandeur;
```

`☕ HorseShop.java`

```java
public class HorseShop {
    public static void intoBestSellers (Horse<? extends Unit> horse) {
        System.out.println("베스트셀러 라인에 추가 - " + horse);
    }

    public static void intoPremiums (Horse<? extends Knight> horse) {
        System.out.println("프리미엄 라인에 추가 - " + horse);
    }

    public static void intoEntryLevels (Horse<? super Knight> horse) {
        System.out.println("보급형 라인에 추가 - " + horse);
    }
}
```

`☕ Main.java`

```java
				HorseShop.intoBestSellers(avante);
        HorseShop.intoBestSellers(sonata);
        HorseShop.intoBestSellers(grandeur);
        
        HorseShop.intoPremiums(avante); // ⚠️ 불가
        HorseShop.intoPremiums(sonata);
        HorseShop.intoPremiums(grandeur);

        HorseShop.intoEntryLevels(avante);
        HorseShop.intoEntryLevels(sonata);
        HorseShop.intoEntryLevels(grandeur); // ⚠️ 불가
```