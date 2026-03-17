# 접근 제어자
![](https://yalco.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F47e1f83e-7c11-4731-b8d7-406967cc71e7%2FUntitled.png?table=block&id=3aecfa2d-4ccb-4ef5-a78a-7528b0c582fc&spaceId=f5787b06-7575-49c2-8c2c-d197061c3d0f&width=1070&userId=&cache=v2)
- 다른 누군가가 쓰게 할 클래스 : 구성요소 중 일부만 밖으로 공개
    - 사용중 오용이나 혼란을 방지
    - ⭐ 캡슐화 _encapsulation_

|접근 가능|`public`|`protected`|`default`|`private`|
|---|---|---|---|---|
|해당 클래스 안에서|✅|✅|✅|✅|
|동일 패키지 안에서|✅|✅|✅||
|동일 패키지 또는 자손 클래스 안에서|✅|✅|||
|다른 패키지 포함 어느 곳에서든|✅||||
### 클래스의 특정 요소를 감추는 이유

- ‘감추는’ 것이 아님 - 코드로 확인 가능
    - 라이브러리 예시 확인
    - 폰도 부숴서 확인할 수 있듯이…
- 작성자의 의도대로 사용하도록 하기 위함
    - 쓰라고 의도한 기능만 공개(IDE의 자동완성 등)하여 혼란 방지
        - 내부적으로 수많은 필드들이 사용된다면?
        - 제한이 오히려 편의를 제공
    - 필드에 부적절한 값이 적용되는 등의 오용 방지
    - 다른 클래스와 복합적으로 사용될 경우 혼선 방지
        - 스마트폰 - PC 연결은 USB 케이블로만…
- 기타 다양한 이유
## Getter와 Setter
```java
public class Product {

    private static double discount = 0.2;
    private static double increaseLimit = 1.2;

    private String name;
    private int price;
}
```
- 메뉴 - 코드 - 생성
    - 윈도우: `alt` + `insert`
    - 맥: `command` + `N`
- `getter 및 setter` 선택
- `name` 과 `price` 선택
```java
	public String getName() {
		return name;
    }

    public void setName(String name) {
        if (name.isBlank()) return;
        this.name = name;
    }

    public int getPrice() {
        return (int) (price * (1 - discount));
    }

    public void setPrice(int price) {
		//  ⭐ this 사용 주의
        int max = (int) (this.price * increaseLimit);
        this.price = price < max ? price : max;
    }
```