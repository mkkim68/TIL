# 유용한 라이브러리 클래스들

### `Math` 클래스

- 각종 수학 계산에 유용한 기능들
- 💡 인스턴스를 만들 수 없음
    - 생성자가 `private` - 코드에서 확인
    - 클래스 필드와 메소드로 사용

`☕ Ex01.java`

```java
				//  ⚠️ 불가. 생성자 확인해 볼 것
        Math mathInst = new Math();
```

```java
				//  ⭐️ 정적 필드들

        //  자연로그의 밑
        double e = Math.E;
        double pi = Math.PI;
```

```java
				// ⭐️ 정적 메소드들

        //  절대값. 숫자 자료형마다 오버로드
        int absInt = Math.abs(-5);
        double absDbl = Math.abs(-3.14);
```

```java
				//  올림, 내림, 반올림
        double ceil = Math.ceil(2.34);
        double floor = Math.floor(4.56);
        double round1 = Math.round(2.34);
        double round2 = Math.round(4.56);
```

```java
				//  큰 수 또는 작은 수 반환. 자료형마다 오버로드
        int largerInt = Math.max(2, 3);
        float smallerFlt = Math.min(1.2f, 3.4f);
```

```java
				//  제곱
        double pow1 = Math.pow(4, 3); // double을 받지만 묵시 형변환
        double pow2 = Math.pow(4, 0.5);
```

```java
				//  0.0 이상 1.0 미만 무작위 수
        double rand1 = Math.random();
        double rand2 = Math.random();
        double rand3 = Math.random();

        //  1에서 10 사이의 무작위 정수
        int _1to10_1 = (int) Math.ceil(Math.random() * 10);
        int _1to10_2 = (int) Math.floor(Math.random() * 10) + 1;
```

```java
				//  ~Exact 메소드들 : 자료형의 범위를 넘기면 오류 발생
        int add1 = Math.addExact(2_147_483_645, 2);
        int add2 = 2_147_483_645 + 3;
        //  int add3 = Math.addExact(2_147_483_645, 3);
```

### `Random` 클래스

```java
				Random random = new Random();
        
        //  아래를 여러 차례 실행해 볼 것

        //  ⭐ 아래를 주석해제한 뒤 실행해 볼 것
        //  random.setSeed(1234);

        int randInt1 = random.nextInt();
        int randInt2 = random.nextInt();
        int randInt3 = random.nextInt();
				// 범위 지정 (이상, 미만)
        int randInt4 = random.nextInt(0, 10);
        int randInt5 = random.nextInt(0, 10);
        int randInt6 = random.nextInt(0, 10);

        double randDbl1 = random.nextDouble();
        double randDbl2 = random.nextDouble();
				// 범위 지정 (이상, 미만)
        double randDbl3 = random.nextDouble(3.14, 5.67);
        double randDbl4 = random.nextDouble(3.14, 5.67);

        boolean randBln1 = random.nextBoolean();
        boolean randBln2 = random.nextBoolean();
```

- 시드 _seed_ 값을 특정 값을 지정하면 이후 랜덤 값들이 일관적으로 나옴
    - 디버깅, 테스트 등에 유용
- 직접 지정하지 않을 시 현재 시각에 따라 자동으로 지정됨
    - 즉 매 회 다른 값이 나옴

### `BigInteger` 클래스

```java
				long maxLong = Long.MAX_VALUE;

        //  💡 BigInteger 클래스
        //  - Long에서 다룰 수 있는 최대 정수 이상의 수를 다룰 수 있음
        BigInteger bigInt1 = new BigInteger("123456789012345678901234567890");
        BigInteger bigInt2 = new BigInteger("987654321098765432109876543210");
```

```java
				BigInteger bigInt3 = bigInt1.add(bigInt2);
        BigInteger bigInt4 = bigInt2.subtract(bigInt1);
        BigInteger bigInt5 = bigInt1.multiply(bigInt2);
        BigInteger bigInt6 = bigInt2.divide(bigInt1);

        int bigIntCompare1 = bigInt1.compareTo(bigInt2);
        int bigIntCompare2 = bigInt2.compareTo(bigInt1);
```

### `BigDecimal` 클래스

```java
				//  부동소수점 오차
        double num1 = 0.2 + 0.3f;
        double num2 = 0.3f * 0.7f;
        double num3 = 0.4 - 0.3;
        double num4 = 0.9f / 0.3;
        double num5 = 0.9 % 0.6;
```

```java
				//  💡 BigDecimal 클래스
        //  - 부동소수점 오차를 해결

        float num6 = new BigDecimal("0.2")
                .add(new BigDecimal("0.3"))
                .floatValue();

        float num7 = new BigDecimal("0.3")
                .multiply(new BigDecimal("0.7"))
                .floatValue();

        float num8 = new BigDecimal("0.4")
                .subtract(new BigDecimal("0.3"))
                .floatValue();

        double num9 = new BigDecimal("0.9")
                .divide(new BigDecimal("0.3"))
                .doubleValue();

        double num10 = new BigDecimal("0.9")
                .remainder(new BigDecimal("0.6"))
                .doubleValue();
```

---

### 문자열 관련 클래스들

`☕ Ex02.java`

```java
				//  💡 StringJoiner : 받은 문자열들을 모아서 열고 닫는 문자열과 함께 join
				//  배열로만 받는 String.join 보다 동적이고 강력함

        String[] strAry = { "감자", "당근", "오이", "양파" };
        StringJoiner strJnr1 = new StringJoiner(",", "<", ">");
        StringJoiner strJnr2 = new StringJoiner(" / ", "{{ ", " }}");

        for (String s : strAry) {
            strJnr1.add(s);
            strJnr2.add(s);
        }

        String joined1 = strJnr1.toString();
        String joined2 = strJnr2.toString();
```

- ⭐️ `StringBuffer` 클래스
    - 자주 변경해야 하는 문자열이 있을 때 적합 _(문자열을 여러 차례 이어붙일 때 등)_
        - `String` : 변경이 있을 때마다 새 종이에 수정본을 작성하는 직원
        - `StringBuffer` : 컴퓨터로 수정작업을 진행하고 마지막에 프린트하는 직원
        - 보다 효율적이고 성능상 유리
    - 문자열 수정 관련 다양한 메소드들
    - 이후 배울 쓰레드 사용에 있어 보다 안전
        - 멀티쓰레드 관련 안전 기능을 제공하므로 성능상 부하
        - ⭐️ 이 기능만 제거한 클래스 : `StringBuilder`
            - 다른 기능들은 동일
            - 단일 쓰레드에서는 `StringBuilder` , 멀티쓰레드에서는 `StringBuffer` 사용

```java
				//  기본적으로 16개의 문자를 저장할 수 있는 공간을 가짐
        StringBuffer strBffr1 = new StringBuffer(); // 기본: 16
        StringBuffer strBffr2 = new StringBuffer(2); // int로 다른 값 지정 가능
        StringBuffer strBffr3 = new StringBuffer("Hello"); // 문자열 길이 + 16

        //  capacity 메소드 : 인스턴스의 문자 저장 공간 확인
        int[] capacities1 = {
                strBffr1.capacity(), strBffr2.capacity(), strBffr3.capacity()
        };

        //  💡 값을 위와 같이 정한 이유:
        //  공간 증축(자원 소모)을 할 일을 최소화하도록 적당한 값을 준 것 뿐
        //  아래와 같이 문자들을 추가하면 필요한 만큼 증축됨
        //  append 메소드 : 인자로 주어진 문자열을 뒤에 이어붙임
        strBffr1.append("안녕하세요~!");
        strBffr2.append("안녕하세요~!");
        strBffr3.append("안녕하세요~!");
        int[] capacities2 = {
                strBffr1.capacity(), strBffr2.capacity(), strBffr3.capacity()
        };

        //  작업을 마친 뒤에는 toString 메소드로 문자열 생성 (최종본 프린트)
        String strBffr3Out = strBffr3.toString();
```

```java
				//  StringBuilder도 동일한 기능들 가짐
        StringBuilder strBldr1 = new StringBuilder("한놈");
        strBldr1.append("두시기");
        
        //  append 메소드는 해당 클래스의 인스턴스 반환
        //  - 메소드 체이닝 가능
        strBldr1
                .append("석삼")
                .append("너구리")
                .append("다섯놈");

				String strBldr1Out = strBldr1.toString();
```

```java
				StringBuilder strBldr2 = new StringBuilder("0123456789");

        String strBldr2Out1 = strBldr2 // 범위의 문자열 지움
                .delete(3, 7).toString();

        String strBldr2Out2 = strBldr2 // 위치의 문자열 삭제
                .deleteCharAt(3).toString();

        String strBldr2Out3 = strBldr2 // 위치에 문자열 추가
                .insert(2, "ABC").toString();

        String strBldr2Out4 = strBldr2 // 범위의 문자열을 치환
                .replace(2, 4, "OneTwo").toString();

        String strBldr2Out5 = strBldr2 // 문자열 뒤집음
                .reverse().toString();

        //  메서드 체이닝으로 한 번에
        String strBldr2ChainOut = new StringBuilder("0123456789")
                .delete(3, 7)
                .deleteCharAt(3)
                .insert(2, "ABC")
                .replace(2, 4, "OneTwo")
                .reverse()
                .toString();
```

```java
				StringBuilder strBldr3 = new StringBuilder("ABCDEFG");

        //  수동으로 저장공간 늘려주기
        //  - 작업할 전체 용량이 초기화 이후 계산되었을 때 유용
        strBldr3.setLength(100);
        int strBldr3Cap = strBldr3.capacity();

        //  주어진 범위만 문자열로 반환
        String strBldr3Substr = strBldr3.substring(2, 5);
```

- ⭐️ `CharSequence`

```java
				//  ⭐️ CharSequence 인터페이스
        //  - String, StringBuffer, StringBuilder 모두 이를 구현
        //  - Integer.parseInt 등의 메서드에 인자 타입으로 널리 사용
        //  - 메소드들 살펴볼 것

        CharSequence cs1 = "ABC";
        CharSequence cs2 = new StringBuffer();
        CharSequence cs3 = new StringBuilder();
```
