# 블록과 스코프
## 블록 block
- 0개 이상의 문 _statement_ 들을 묶은 단위
- 제어문, 함수, 클래스 등에 사용
- 새로운 **스코프** 생성
## 메소드와 클래스의 스코프
- 클래스 메소드에서 인스턴스 필드 사용 불가
- 클래스 내 필드의 스코프 : 해당 클래스 안
- 메소드 내 변수의 스코프 : 해당 메소드 안
### 자바에서는 바깥의 변수 재선언 불가
- 자바스크립트 등의 언어와 달리…
### 인스턴스와 필드는 다른 영역으로 간주
```java
public class Ex04 {

    public static void main(String[] args) {
        new Ex04().printKings();
    }

    String king = "사자";

    void printKings () {
        String king = "여우"; // 💡 그럼 이건 뭔가요??

        //  ⭐️ 인스턴스의 필드는 다른 영역으로 간주
        System.out.printf(
                "인스턴스의 왕은 %s, 블록의 왕은 %s%n",
                this.king, king
        );
    }
}
```