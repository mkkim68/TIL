# 익명 클래스
## 기본
- 다른 클래스나 인터페이스로부터 상속받아 만들어짐
    - 주로 오버라이드한 메소드를 사용
- 한 번만 사용되고 버려질 클래스
    - 따로 클래스명이 부여되지 않음
    - 이후 다시 인스턴스를 생성할 필요가 없으므로
- 이후 배울 람다식이 나오기 전 널리 사용
## 예시
### `📁 ex01`

`☕ Main.java`

```java
		//  💡 와일드카드로 임포트 - import sec05.chap08.ex01.*;

        YalcoGroup store1 = new YalcoChicken("울산");
        YalcoGroup store2 = new YalcoCafe("창원", true);

        YalcoGroup store3 = new YalcoGroup (1, "포항") {
            
			//  원본 메소드에 public 추가
			@Override
            public void takeOrder() {
                System.out.printf(
                        "유일한 얄코과메기 %s 과메기를 주문해주세요.%n",
                        super.intro()
                );
            }

            public void dryFish () {
                System.out.println("과메기 말리기");
            }
        };

        String store3Intro = store3.intro();
        store3.takeOrder();
        //store3.dryFish // ⚠️ 불가

        System.out.println("\\n- - - - -\\n");

        for (YalcoGroup store : new YalcoGroup[] {store1, store2, store3}) {
            store.takeOrder();
        }
```

- 💡 익명클래스의 인스턴스는 상속받거나 오버라이드 된 메소드만 호출 가능

---

### `📁 ex02`

- 안드로이드 자바로 개발시 볼 수 있던 코드

`☕ OnClickListener.java`

```java
public interface OnClickListener {
    void onClick ();
}
```

`☕ Button.java`

```java
public class Button {
    String name;
    public Button(String name) {
        this.name = name;
    }

		//  ⭐️ 인터페이스를 상속한 클래스 자료형
    private OnClickListener onClickListener;
    public void setOnClickListener(OnClickListener onClickListener) {
        this.onClickListener = onClickListener;
    }

    public void func () {
        onClickListener.onClick();
    }
}
```

`☕ Main.java`

```java
        Button button1 = new Button("Enter");
        Button button2 = new Button("CapsLock");
        Button button3 = new Button("ShutDown");

				//  ⭐️ IDE에서 회색으로 표시 : 이후 배울 람다로 대체
        button1.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick() {
                System.out.println("줄바꿈");
                System.out.println("커서를 다음 줄에 위치");
            }
        });

        button2.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick() {
                System.out.println("기본입력 대소문자 전환");
            }
        });

        button3.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick() {
                System.out.println("작업 자동 저장");
                System.out.println("프로그램 종료");
            }
        });

        for (Button button : new Button[] {button1, button2, button3}) {
            button.func();
        }
```