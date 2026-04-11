# 2. Wrapper 클래스들

![](https://yalco.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd245c660-2580-4283-ad21-22f18f409523%2F%25E1%2584%2583%25E1%2585%25A2%25E1%2584%258C%25E1%2585%25B5_27_%25E1%2584%2589%25E1%2585%25A1%25E1%2584%2587%25E1%2585%25A9%25E1%2586%25AB.png?table=block&id=d6921009-95eb-4c12-9640-f49e567d77ea&spaceId=f5787b06-7575-49c2-8c2c-d197061c3d0f&width=1020&userId=&cache=v2)

🦾 _토니와 아이언맨 수트 (?)_

- 각 원시 자료형에는 그에 해당하는 **래퍼 클래스**가 있음
    - 해당 자료형에 관련된 클래스/인스턴스 기능들을 제공
    - 클래스 인스턴스를 받는 곳에 활용
        - 다음 강에서 배울 제내릭 등…
- 각 자료형의 원시값은 해당 래퍼 클래스의 인스턴스와 서로 변환 가능
- 💡 원시값의 존재 이유 : 더 높은 성능
    - 대신 순수한 객체지향 언어는 아니게 됨…

`☕ Ex01.java`

```java
				//  원시 자료형
        int int1 = 123;
        double dbl1 = 3.14;
        char chr1 = 'A';
        boolean bln1 = true;

        //  ⭐ 해당 래퍼 클래스의 인스턴스
        //  기존의 생성자 방식
        //  ⚠️ 오늘날에는 deprecated - 성능상 좋지 않음
        Integer int2 = new Integer(123);
        Double dbl2 = new Double(3.14);
        Character chr2 = new Character('A');
        Boolean bln2 = new Boolean(true);

        //  💡 아래의 클래스 메소드들이 권장됨
        Integer int3 = Integer.valueOf(123);
        Double dbl3 = Double.valueOf(3.14);
        Character chr3 = Character.valueOf('A');
        Boolean bln3 = Boolean.valueOf(true);
```

- 각각 `value` 란 필드를 가진 클래스 인스턴스임 확인

|원시 자료형|래퍼 자료|
|---|---|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
|char|Character|
|boolean|Boolean|

- ⭐️ 숫자 자료형들 _(`Integer` , `Double` 등…)_ - 추상 클래스 `Number` 에서 상속
    - IDE 기능으로 `Number` 확인해 볼 것

```java
				Number num1 = int1;
        Number num2 = dbl1;
```

---

### 박싱과 언박싱

- 원시값을 래퍼 클래스의 인스턴스로 **boxing**
- 래퍼 클래스의 인스턴스를 원시값으로 **unboxing**

`☕ Ex02.java`

```java
				//  💡 박싱 : 원시값을 래퍼 클래스의 인스턴스로
        //  ⭐ 과거에는 생성자를 사용했으나 deprecated
        int intPrim1 = 123;
        Integer intInst1 = Integer.valueOf(intPrim1);

        char chrPrim1 = 'A';
        Character chrInst1 = Character.valueOf(chrPrim1);

        //  💡 언박싱 : 래퍼 클래스의 인스턴스를 원시값으로
        Double dblInst1 = Double.valueOf(3.14);
        double dblPrim1 = dblInst1.doubleValue();

        Boolean blnInst1 = Boolean.valueOf(true);
        boolean blnPrim1 = blnInst1.booleanValue();
```

### 오토박싱과 언박싱

- 명시적으로 박싱/언박싱하지 않아도 컴파일러가 자동으로 처리
- 성능상으로는 떨어지므로 자주 사용하지는 _(반목문 안에서 등)_ 말 것

```jsx
		static int add(Integer a, Integer b) { return a + b; }
```

```jsx
				//  💡 오토박싱
        Integer intInst2 = 234;
        Double dblInst2 = 1.414213;

        //  💡 오토언박싱
        char chrPrim2 = Character.valueOf('B');
        boolean blnPrim2 = Boolean.valueOf(false);

        //  원시값과 래핑 클래스 인스턴스끼리의 연산
        int intPrim2 = intPrim1 + intInst2;
        Integer intInst3 = intPrim2 + intInst2;

        //  메소드 등 사용처들에 혼용 가능
        Integer intInst4 = add(3, 5);
```

---

### 래퍼 클래스의 대표적/유용한 메소드들

- IDE의 기능을 통해 다른 메소드들도 둘러볼 것

`☕ Ex03.java`

```jsx
				//  💡 숫자 클래스 메소드들

        //  CharSequence로부터 인스턴스 반환
        //  ⭐ CharSequence : String 등이 구현하는 인터페이스
        Integer int1 = Integer.valueOf("123"); // 문자열로부터 인스턴스 반환

        //  CharSequence로부터 원시값 반환
        //  💡 다른 숫자, 불리언 래퍼 자료형들에도 존재 (parseDouble, parseBoolean...)
        int int2 = Integer.parseInt("123"); // 원시값 반환

        //  parseInt(CharSequence, 진수)
        //  정수 자료형들에만 존재
        //  ⭐ CharSequence : String 등이 구현하는 인터페이스
        int int_123_oct = Integer.parseInt("123", 8);
        int int_123_dec = Integer.parseInt("123", 10);
        int int_123_hex = Integer.parseInt("123", 16);

        //  parseInt(CharSequence, 시작위치, 끝위치, 진수)
        int int3 = Integer.parseInt("1234567", 3, 5, 10);
```

```java
				//  💡 문자 클래스 메소드들

        String strSample = "Ab가1 .";
        for (int i = 0; i < strSample.length(); i++) {
            Character c = strSample.charAt(i);
            System.out.printf(
                    "[%c] : L: %b, U: %b, L: %b, D: %b, S: %b%n",
                    c,
                    Character.isLetter(c),
                    Character.isUpperCase(c),
                    Character.isLowerCase(c),
                    Character.isDigit(c),
                    Character.isSpaceChar(c)
            );
        }
```

```java
				//  💡 인스턴스 메소드들

        //  문자열 반환 (Object에서 오버라이드)
        String intStr = int1.toString();
        String dblStr = Double.valueOf(3.14).toString();
        String blnStr = ((Boolean) false).toString();
        String chrStr = new Character('A').toString();
```

```java
				//  인스턴스끼리의 value 비교
        Integer intA = 12345;
        Integer intB = 12345;

        boolean compByOp1 = intA == intB; // ⚠️ 값은 같으나 다른 참조
        boolean compByEq1 = intA.equals(intB);

        Short srtA = 12345;

        //  ⚠️ 자료형이 다르면 false 반환 (메소드 코드 확인)
        boolean compByOp2 = intA.equals(srtA);
```

```java
				//  숫자 자료형 간 변환 - Number의 추상 메소드들

				Byte int1Byt = int1.byteValue();
        Double int1Dbl = int1.doubleValue();

        Integer int4 = 123456789;
        Byte int4Byt = int4.byteValue(); // ⚠️ 자료형보다 값이 큼

        Float flt1 = 1234.5678f;
        Integer flt1Int = flt1.intValue(); // ⚠️ 소수점 이하 버림
        Short int1DblSrt = int1Dbl.shortValue();
```