# 메인 메소드
## 기본
- 자바 프로그램의 시작점
    - 작성된 모든 코드들의 엔트리
- 메인 메소드가 포함된 클래스를 통해 프로그램을 실행
## 예시
`☕ Ex01.java`

```java
package sec06.chap05; // ⭐️ 파일이 든 폴더에서 실행하려면 지울 것!

public class Ex01 {
    public static void main(String[] args) {
        System.out.println("메인 메소드 실행");
    }
}
```

- `src` 디렉토리에서 실행

```bash
javac -encoding UTF-8 sec06/chap05/Ex01.java
```

- `.class` 파일 생성
- 실행 위치와 패키지 정보를 맞출 것!

```bash
java sec06/chap05/Ex01
```

- 파일 실행됨
- ⭐️ 메인 메소드를 없애거나 이름/속성을 변경하고 실행해 볼 것

---

### 매개변수 전달하여 활용하기

`☕ Ex02.java`

```java
package sec06.chap05;

public class Ex02 {
    public static void main(String[] args) {

        for (String arg : args) {
            System.out.println(arg);
        }
    }
}
```

- 터미널 `src` 디렉토리에서 실행

```bash
javac sec06/chap05/Ex02.java
```

```bash
java sec06/chap05/Ex02 한놈 두시기 석삼 너구리 "다섯놈 육개장 칠면조"
```

- IntelliJ에서 실행
    - Edit Configuration 에서 메인 파일 설정, 매개변수 입력
        - 설정의 이름을 지정하여 저장하면 유용
    - 해당 설정으로 프로젝트 실행
        - 여러 설정 중에 선택하여 실행 가능

---

`☕ Ex03.java`

```java
				if (args.length < 2) {
            System.out.println("메뉴와 맵기를 모두 입력해주세요.");
            return;
        }

        String menuName = args[0];
        String spicyLevel = args[1];

        if (spicyLevel.length() != 1) {
            System.out.println("맵기를 한 자리 숫자로 입력해주세요.");
            return;
        }
        if (!"0123456789".contains(spicyLevel)) {
            System.out.println("맵기는 숫자로 입력해주세요.");
            return;
        }

        System.out.printf("%s 맵기 강도 %s로 주문%n", menuName, spicyLevel);
```

---