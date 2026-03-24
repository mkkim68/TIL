# 내부 클래스
## 기본
- 다른 클래스 안에 선언되는 클래스
- 크게 4 종류가 있음
    - 멤버 인스턴스
    - 정적 내부 클래스
    - 메소드 안에 정의된 클래스
    - 익명 클래스
## 내부 클래스를 사용하는 이유
- 보다 강력한 캡슐화
    - 외부/내부 클래스간의 관계가 긴밀할 때 사용
- 적절히 사용시 유지보수가 용이하고 가독성을 높여줌
    - 과하게 사용되면 클래스 비대화
## 예시
### `📁 ex02`

`☕ YalcoChicken.java`

```java
public class YalcoChicken {
    private String name;
    public YalcoChicken (String name) {
        this.name = name;
    }

    //  매장신설 TF팀 - 본사에서 창설
    public static class LaunchTF {
        private String title;
        private String leader;

        public LaunchTF(String title, String leader) {
            this.title = title;
            this.leader = leader;
        }

        public YalcoChicken launch () {
			//  ⚠️ 인스턴스 필드는 사용 불가
            //  System.out.println(this.name);
            return new YalcoChicken(title);
        }
    }

    //  매장마다의 기프트 - 매장에서 배부
    class Gift {
        private String message;

        public Gift(String to) {
            this.message = "From 얄코치킨 %s점 to %s님"
                    .formatted(name, to);
        }
    }

    public Gift getGift (String to) {
        return new Gift(to);
    }
}
```

`☕ Main.java`

```java
				YalcoChicken.LaunchTF launchTF1 = new YalcoChicken.LaunchTF("마산", "김영희");
        YalcoChicken.LaunchTF launchTF2 = new YalcoChicken.LaunchTF("영월", "이철수");

        YalcoChicken store1 = launchTF1.launch();
        YalcoChicken store2 = launchTF2.launch();

        YalcoChicken.Gift [] gifts = {
                store1.getGift("홍길동"),
                store1.getGift("전우치"),
                store2.getGift("옥동자")
        };
```

- 외부에 클래스를 따로 두는 것보다 관리 용이성과 가독성이 높아짐 확인
    - `YalcoChickenLaunchTF`, `YalcoChickenGift`를 따로 두어야 했다면?