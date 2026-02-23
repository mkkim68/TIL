# 클래스(정적) 필드와 메소드
## ex01
- `YalcoChicken.java`
```java
public class YalcoChicken {

    //  ⭐️ 클래스/정적 필드와 메소드들 : 본사의 정보와 기능
    //  인스턴스마다 따로 갖고 있을 필요가 없는 것들에 사용
    static String brand = "얄코치킨";
    static String contact () {
        //  ⚠️ 정적 메소드에서는 인스턴스 프로퍼티 사용 불가
        //  System.out.println(name);

        return "%s입니다. 무엇을 도와드릴까요?".formatted(brand);
    }

    int no;
    String name;

    YalcoChicken(int no, String name) {
        this.no = no;
        this.name = name;
    }

    String intro () {
        //  💡 인스턴스 메소드에서는 정적 프로퍼티 사용 가능
        return "안녕하세요, %s %d호 %s점입니다."
                .formatted(brand, no, name);
    }
}
```
- `Main.java`
```java
		//  💡 클래스 필드와 메소드는 인스턴스를 생성하지 않고 사용
        String ycBrand = YalcoChicken.brand;
        String ycContact = YalcoChicken.contact();

        // ⚠️ 인스턴스 메소드는 불가
        //  String ycName = YalcoChicken.name;
        //  String ycIntro = YalcoChicken.intro();

        YalcoChicken store1 = new YalcoChicken(3, "판교");
        String st1Intro = store1.intro();

        //  인스턴스에서는 클래스의 필드와 메소드 사용 가능
        //  ⚠️ 편의상 기능일 뿐, 권장하지 않음 (혼란 초래. IDE에서 자동완성 안 됨 주목)
        String st1Brand = store1.brand;
        String st1Contact = store1.contact();
```
![](https://yalco.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9c99cb4f-2066-4b93-af09-dd1eede22e3d%2F_%25EB%258C%2580%25EC%25A7%2580_27.png?table=block&id=3ac7ac59-c3dd-4912-a1ba-9a207ea99c4e&spaceId=f5787b06-7575-49c2-8c2c-d197061c3d0f&width=1170&userId=&cache=v2)
- 클래스(정적 _static_) 요소: 메모리 중 한 곳만 차지
- 인스턴스 요소들: 각각이 메모리에 자리를 차지
    - 각각의 자신만의 프로퍼티 값을 가지고 있음