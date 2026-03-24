# 패키지
- 자바 프로젝트의 디렉토리(폴더) - 패키지로 불리게 됨
    - 일정 규모 이상의 프로그램을 적절히 모듈화
    - 패키지 정보: 클래스의 구성요소 중 하나
- 클래스명의 중복을 피하기 위해 사용
    - 예: `Button` 클래스 - JRE의 동명 클래스 등 확인
- 빌드의 결과도 패키지의 구조를 따름
    - 이전 예제들의 `out` 폴더 확인할 것
---
### `📁 pkg1`

`☕ Parent.java`

```java
public class Parent {
    private int a = 1;
    int b = 2;
    protected int c = 3;
    public int d = 4;
}
```

`☕ Child.java`

```java
public class Child extends Parent {
    //  Parent와 같은 패키지
    //  int aa = a; // ⚠️ 불가
    int bb = b;
    int cc = c; // 💡 protected - 같은 패키지, 상속관계
    int dd = d;
}
```

`☕ Friend.java`

```java
public class Friend {
    //  Parent와 같은 패키지
    Parent parent = new Parent();

    //  int aa = new Parent().a; // ⚠️ 불가
    int bb = parent.b;
    int cc = parent.c; // 💡 protected - 같은 패키지, 비 상속관계
    int dd = parent.d;
}
```

### `📁 pkg2`

`☕ Child.java`

```java
//  상단에 임포트 필요 

public class Child extends Parent {
    //  Parent와 다른 패키지
    //  int aa = a; // ⚠️ 불가
    //  int bb = b; // ⚠️ 불가
    int cc = c; // 💡 protected - 다른 패키지, 상속관계
    int dd = d;
}
```

### `📁 pkg3`

`☕ Cls1.java`, `☕ Cls2.java`, `☕ Cls3.java`

```java
public class Cls1 {
    //  자유롭게 작성
}
```

### `📁 pkg4`

`Main.java`

```java
import sec06.chap02.pkg1.Parent;
import sec06.chap02.pkg3.*; // ⭐️ 와일드카드

public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();

        //  ⭐️ 패키지가 다른 동명의 클래스들을 불러올 경우
        sec06.chap02.pkg1.Child child1 = new sec06.chap02.pkg1.Child();
        sec06.chap02.pkg2.Child child2 = new sec06.chap02.pkg2.Child();

        Cls1 cls1 = new Cls1();
        Cls2 cls2 = new Cls2();
        Cls3 cls3 = new Cls3();
    }
}
```

---

### `src` 폴더에서 명령 입력해 볼 것

- 최상위 패키지가 포함된 폴더일 것
- 다른 위치 _(바깥쪽이든 안쪽이든)_ 에서는 디렉토리 맞춰도 오류 발생

```bash
javac sec06/chap02/pkg4/Main.java
```

- `.class` 파일들 생성 결과 확인

### `.class` 파일들 지운 뒤, 같은 폴더에서 아래의 명령 입력해 볼 것

```bash
javac -d sec06/chap02/compileds sec06/chap02/pkg4/Main.java
```

- 원하는 위치에 프로젝트 구조에 따른 `.class` 파일들 생성할 수 있음 확인

---

### ⭐️ 리펙토링

- IntelliJ에서 클래스들을 다른 패키지로 옮겨 볼 것
- 파일의 위치 변경이 패키지 정보에도 반영되어야 함

---

### 프로젝트 패키지명 작명

- 인텔리제이에서 새 프로젝트 - Maven 또는 Gradle - 고급 옵션에서 예시
- 본인/또는 회사의 도메인 _(있을 경우)_ 권장
    - `kr.yalco.calculator`
        - _한국에 있는 얄코란 사람/회사가 만든 계산기 프로그램_
        - 규모, 주체, 용도 등을 파악 가능
        - 다른 프로젝트들에 사용될 시…
- `java`, `javax` 가 맨 앞에 올 수 없음 _(JRE 라이브러리와 중복)_
    - `src` 폴더 안에 만들고 클래스 넣어 확인해 볼 것
- 식별자 명명 규칙 따름
    - 소문자로 시작하는 것이 컨벤션

---

### ⭐️ `java.lang` 패키지

- 자바 라이브러리에 기본으로 포함
    - 프로그래밍에 널리 사용되는 핵심적인 클래스들
- 임포트하지 않아도 되는 패키지
    - `System`, `String` 등을 임포트하지 않아도 되는 이유
    - 다른 라이브러리 패키지들은 임포트해야 함

### `📁 pkg5`

`☕ Main.java`

```java
				//  java.lang 패키지에 속한 기본 라이브러리 클래스들
        System.out.println("이 클래스들은 왜 임포트를 안 해도 될까요?");
        Object object = new Object();
        String str = new String("java.lang 패키지 소속이라 그럼");
        Integer integer;
        Math math;

        //  다른 패키지에 속한 기본 라이브러리 클래스들
        ArrayList arrayList;
        Calendar calendar;
        Optional optional;
        Iterator iterator;
        InputStream inputStream;
        Serializable serializable;
        Stream stream;
        Button button;
```