# 9. 날짜와 시간 관련 클래스들

- 예전에는 [`java.util`](http://java.util.Date) 패키지의 `Date`, `Calendar`를 많이 사용했음
    - 자바8 이전의 프로젝트를 사용한다면 **Joda-Time** 라이브러리 사용
        - 외부 라이브러리, 영국의 [**Joda.org**](http://Joda.org) 에서 제작
        - 보다 많은 기능들을 제공했음
        - `org.joda.time` 패키지
- 자바8부터는 `java.time` 패키지의 클래스들을 사용
    - **Joda-Time** 기반으로 제작 - _기능 유사_
    - `java.util`의 클래스들보다 우수
        - 보다 직관적인 사용법
        - 보다 정확한 시간 계산
        - 인스터스 변경 불가 - 멀티쓰레드상 안전
        - 더 다양한 기능들 제공

`☕ Main.java`

```java
				//  ⭐️ java.time의 클래스들은 생성자 대신
        //  - 필요에 따라 적합한 클래스 메소드로 인스턴스 생성

        //  💡 현재 날짜
        LocalDate today = LocalDate.now();
        System.out.println(today);

        //  💡 현재 시간
        LocalTime thisTime = LocalTime.now();
        System.out.println(thisTime);

        //  💡 현재 시간과 날짜
        LocalDateTime now = LocalDateTime.now();
        System.out.println(now);

        //  ⭐️ now 메서드 : 현재의 시간/날짜 정보를 가진
        //  해당 클래스의 인스턴스를 반환
				//  시스템(컴퓨터)의 시계를 기준으로 함
```

```java
				System.out.println("\\n- - - - -\\n");

        LocalDate christmas23 = LocalDate.of(2023, 12, 25);
        System.out.println(christmas23);

        LocalTime lunchTime = LocalTime.of(12, 30);
        LocalTime lunchTimeDetailed = LocalTime.of(
                12, 30, 0, 0
        ); // 초, 나노초까지 더할 수 있음
        System.out.println(lunchTime);

        LocalDateTime familyDinner = LocalDateTime.of(
                2023, 12, 25, 18, 00
        );
        System.out.println(familyDinner);
        //  LocalDateTime 인스턴스는 LocalDate와 LocalTime 인스턴스의 조합으로
        //  만들어짐 클래스 코드에서 확인 (of 메소드)
```

```java
				System.out.println("\\n- - - - -\\n");

        //  ⭐️ java.time의  Local... 클래스 인스턴스들은 불변
        //  - 생성자 사용이 금지된 것은 인스턴스 생성을 제한하기 위함
        //  - of 메소드를 사용하여, 적절할 때만 생성된 것을 받도록

        //  💡 주어진 차이만큼의 시간이나 날짜를 '새로 만들어' 반환
        today.plusDays(1); // ⭐️ 기존 인스턴스는 변하지 않음
        LocalDate tomorrow = today.plusDays(1);
        LocalDate yesterday = today.minusDays(1);

        for (LocalDate day : new LocalDate[] {today, tomorrow, yesterday}) {
            System.out.println(day);
        }
```

```java
				LocalDate threeMonthsLater = today.plusMonths(3);
        LocalDate tenYearsBefore = today.minusYears(10);

        //  💡 메소드 체이닝 사용

        LocalTime hourAndHalfLater = thisTime
                .plusHours(1)
                .plusMinutes(30);

        LocalDateTime randomPast = now
                .minusYears(1)
                .plusMonths(2)
                .minusDays(3)
                .plusHours(4)
                .minusMinutes(5)
                .plusSeconds(6)
                .minusNanos(7);
```

```java
				System.out.println("\\n- - - - -\\n");

        //  💡 ZonedDateTime : 시간대 정보를 추가로 가짐
        //  - '이 컴퓨터가 어느 시간대의 시간을 따르는가'
        ZonedDateTime nowHere = ZonedDateTime.now();
        System.out.println(nowHere);

        //  💡 현재 시간대 구하기
        String hereZone = nowHere.getZone().toString();

        //  💡 특정 지역의 특정 시간
        ZonedDateTime newYorkNewYear = ZonedDateTime.of(
                2023, 1, 1,
                0, 0, 0, 0,
                ZoneId.of("America/New_York")
        ); //  ⭐️ ZoneId 클래스에서 지역들 목록 볼 것
        //  서울에서는 오전 5시
```

```java
				System.out.println("\\n- - - - -\\n");

        //  시간차이 구하기

        //  💡 Period 클래스 : 두 날짜 사이의 간격을 다루는 클래스
        LocalDate childrensDay30 = LocalDate.of(2030, 5, 5);
        Period toChldDay30 = Period.between(today, childrensDay30);
        int[] toChldDay30inUnits = {
                toChldDay30.getYears(),
                toChldDay30.getMonths(),
                toChldDay30.getDays()
        }; // 연, 월, 일 부분 각각 표시
```

```java
				LocalDateTime year2000 = LocalDateTime.of(
                2000, 1, 1, 0, 0
        );

        //  💡 Duration 클래스 : 두 시간 사이의 간격을 다루는 클래스
        Duration from2000 = Duration.between(year2000, now);
        long[] from2000inUnits = {
                from2000.toDays(),
                from2000.toHours(),
                from2000.toMinutes(),
                from2000.toSeconds()
        }; // 일, 시, 분, 초 등의 단위로 환산 (위의 Period와 다름)
```

```java
				//  ⭐️ 시간 표기형식 지정하기
        //  - DateTimeFormatter 클래스의 ofPattern 메소드 사용
        DateTimeFormatter formatter1 =
                DateTimeFormatter.ofPattern("1. yyyy-MM-dd");

        DateTimeFormatter formatter2 =
                DateTimeFormatter.ofPattern("2. yyyy/MM/dd HH:mm:ss");

        DateTimeFormatter formatter3 =
                DateTimeFormatter.ofPattern("3. yy.MM.dd");

        DateTimeFormatter formatter4 =
                DateTimeFormatter.ofPattern("4. dd/MM/yyyy hh a");

        DateTimeFormatter formatter5 =
                DateTimeFormatter.ofPattern("5. yyyy년 MM월 dd일 HH시");

        //  DateTimeFormatter 클래스의 코드에서 각 형식 요소 확인

        for (DateTimeFormatter formatter : new DateTimeFormatter [] {
                formatter1,
                formatter2,
                formatter3,
                formatter4,
                formatter5,
        }) {
            //  💡 형식에 따라 시간을 문자열로
            System.out.println(now.format(formatter));
        }
```

```java
				//  역 : 문자열에서 시간 인스턴스로

        String christmas25str = "2025-12-25";
        DateTimeFormatter formatterA =
                DateTimeFormatter.ofPattern("yyyy-MM-dd");
        LocalDate christmas25 = LocalDate
                .parse(christmas25str, formatterA);
        //  ⚠️ 시간 정보는 없으므로 LocalDateTime으로 하면 오류 발생

        String christmas25dinnerStr = "2025/12/25 18:00:00";
        DateTimeFormatter formatterB =
                DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
        LocalDateTime christmas25dinner = LocalDateTime
                .parse(christmas25dinnerStr, formatterB);
```