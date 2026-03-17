# 상속
## 기본
```java
public class YalcoChicken {
    protected int no;
    protected String name;

    public YalcoChicken (int no, String name) {
        this.no = no;
        this.name = name;
    }

    public void takeHallOrder () {
        System.out.printf("%d호 %s점 홀 주문 받음%n", no, name);
    }
}
```
### 드라이브스루를 갖춘 얄코치킨의 클래스를 만든다면?
- 기존 얄코치킨 클래스의 모든 필드와 메소드 포함
- 드라이브스루 관련 필드와 메소드 추가
- ⭐ `YalcoChicken` 을 부모로 하는 자식 클래스 `YalcoChickenDT` 만들기
    - `extends` 연산자 사용
```java
public class YalcoChickenDT extends YalcoChicken {
    private boolean driveThruOpen = true;

    public YalcoChickenDT(int no, String name) {
        super(no, name); // 다음 예제에서 다룰 것
    }

    public void setDriveThruOpen(boolean driveThruOpen) {
        this.driveThruOpen = driveThruOpen;
    }

    public void takeDTOrder () {
        System.out.printf(
                "%d호 %s점 드라이브스루 주문 %s%n",
                no, name,
                (driveThruOpen ? "받음" : "불가")
        );
    }
}
```
- Main.java
```java
		YalcoChickenDT dtStore1 = new YalcoChickenDT(108, "철원");

        dtStore1.takeHallOrder();

        dtStore1.takeDTOrder();
        dtStore1.setDriveThruOpen(false);
        dtStore1.takeDTOrder();
```
- 디버그 모드로 `dtStore1` 인스턴스 살펴볼 것
    - 부모 클래스의 요소들 갖고 있음 확인 - **상속** _inheritance_
- 부모 클래스의 `protected` 필드들을 `private` 으로 바꿔 볼 것
    - 💡 상속이 안 되는 것은 아님 - 자식클래스의 코드에서 사용하지 못할 뿐
## 메소드 오버라이딩
- 부모가 가진 같은 이름의 메소드를 자식이 다르게 정의
    - _‘저는 제 방식대로 하겠습니다.’_
- 오버로딩과 혼동하지 말 것
### 오버라이드 편의기능
- 메뉴 - 코드 - 생성 - 메소드 재정의 선택 (생성자까지 진행)
### `super` 부모의 생성자/메소드 호출
- 부모 클래스에 생성자가 작성되었을 시
    - 자식 클래스에도 생성자 작성 필요
        - 생성자를 제거해 볼 것
    - `super` 를 사용해서 부모의 생성자를 먼저 호출
        - 이후 추가로 필요한 내용 작성
        - 즉 부모의 인스턴스부터 생성 후 이를 기반으로 자식 인스턴스 생성
        - 자식 클래스의 생성자는 `super` 로 시작해야 함
            - 순서 바꿔 볼 것
- 부모의 기타 메소드를 자식 클래스에서 사용시 앞에 `super.` 를 붙임
    - 즉 `super` 는 부모 클래스의 인스턴스(실존하지 않음 - 자신 안의 부모 유전자)를 가리킴
        - `this` 가 해당 클래스의 인스턴스를 가리키듯…
    - 어떤 메소드에서든, 어떤 위치에서든 사용 가능
### `@Override` 어노테이션
- 부모의 특정 메소드를 오버라이드함을 명시
    - 없어도 오류가 나지는 않음
    - 붙였는데 메소드명이 다를 시 오류 (실수 방지)
### 부모 클래스에 명시된 생성자가 없는 경우
- 자식 클래스에서도 작성할 필요 없음
### 💡 상속의 또 다른 용도
- 자신이 만든 것이 아닌 클래스를 커스터마이즈 _(마개조)_