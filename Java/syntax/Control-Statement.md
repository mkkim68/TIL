# 제어문
## 조건문
### if/else
- 주어진 boolean 값에 따라 명령문 실행 여부 결정
```java
		boolean open = true;
		int saleFrom = 10, saleTo = 20;
		int today = 15;
		
		//  💡 if : 괄호 안의 boolean 값이 true면 다음 명령 실행
		if (open) System.out.println("영업중");
		if (!open) System.out.println("영업종료");
		
		//  💡 실행할 명령이 한 줄 이상일 경우 블록 사용
		if (today >= saleFrom && today <= saleTo) {
			System.out.println("세일중입니다.");
			System.out.println("전품목 20% 할인");
		}
		
		//  💡 else : if문 안의 boolean 값이 false일 경우 실행
		if (open) {
			System.out.println("영업중");
		} else {
			System.out.println("영업종료");
		}
```
### else if
```java
		int score = 85;

        //  💡 else if : 첫 if문이 false일 때 다른 조건을 연속 사용
        //  else만 사용하는 것은 맨 마지막에
        if (score > 90) {
            System.out.println('A');
        } else if (score > 80) {
            System.out.println('B');
        } else if (score > 70) {
            System.out.println('C');
        } else if (score > 60) {
            System.out.println('D');
        } else {
            System.out.println('F');
        }
```
- 가독성이 좀 떨어짐 -> 개선 버전
```java
		int score = 85;

        //  ⭐ 보다 가독성 좋은 방식
        //  return문: 해당 메소드를 종료하고 빠져나옴
        
        if (score > 90) {
            System.out.println('A');
            return;
        }
        if (score > 80) {
            System.out.println('B');
            return;
        }
        if (score > 70) {
            System.out.println('C');
            return;
        }
        if (score > 60) {
            System.out.println('D');
            return;
        }
        System.out.println('F');
```
### switch
```java
		byte fingersOut = 2;

        //  💡 switch : 괄호 안에 기준이 될 변수를 받음
        //  가능한 자료형: byte, short, int, char, String, enum(이후 배움)
        
        switch (fingersOut) {

            //  💡 case : 기준에 일치하는 case로 바로 이동
            //  💡 break : switch문 실행을 종료
            //  💡 default: 해당하는 case가 없을 때 - 마지막에 작성

            case 2:
                System.out.println("가위");
                break;
            case 0:
                System.out.println("바위");
                break;
            case 5:
                System.out.println("보");
                break;
            default:
                System.out.println("무효");
        }
```
- switch와 case 자료형 같게
- [!] break가 없으면 모든 case를 다 출력함
## 반복문
- 주어진 조건이 충족되는 동안 특정 작업을 반복
```java
		for (int i = 0; i < 10; i++) {
            System.out.println(i); // 🔴
        }
```
![](https://yalco.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb687d2fc-416e-4442-a4df-0b998e5eb363%2F%25E1%2584%2583%25E1%2585%25A2%25E1%2584%258C%25E1%2585%25B5_9.png?table=block&id=58e0f033-b5a8-4d04-bf86-06588555a860&spaceId=f5787b06-7575-49c2-8c2c-d197061c3d0f&width=1420&userId=&cache=v2)
- 실행 과정
    1. 루프 안에서 사용할 변수 초기화
    2. 루프를 실행하기 위한 조건 확인
    3. 조건을 충족시 실행할 내용
    4. 각 루프가 끝날때마다 이행할 내용
- 1번 이후 2를 충족할 동안 2~4 반복
- 변수명은 원하는대로 사용 가능
    - 일반적으로 기본형에는 `i` 를 많이 사용 - _문맥에 따라 index를 뜻함_
### 여러 변수 사용 가능
```java
		//  💡 쉼표로 구분하여 여럿 사용 가능
        //  ⚠️ 변수의 자료형은 한 종류만 가능 (혼용 안 됨)
        for (byte a = 0, b = 10; a <= b;) {
            System.out.printf("a: %d, b: %d%n", a++, b--);
        }
```
### 무한 루프
```java
		//  종료조건이 없는 for 루프
        for (;;) {
            System.out.println("영원히");
        }
        System.out.println("닿지 않아"); // ⚠️ 실행되지 않음
```
- 컴파일 자체가 실패됨
```java
		//  종료조건을 만족시키지 못하는 무한루프
        for (int i = 0; i < 10; i++) {
            System.out.println("그래도");
            i--;
        }
        System.out.println("닿지 않아"); // ⚠️ 실행되지 않음
```
- 컴파일러가 판단 불가능
- 무한루프는 프로그램을 정지시킴
### 배열의 루프
#### 기본
```java
		//  💡 배열 순환 (기본적인 방법)
		for (int i = 0; i < multiOf4.length; i++) {
            System.out.println(multiOf4[i]);
        }
```
#### for each
```java
		//  💡 for each 문법 - 배열이나 이후 배울 콜랙션 등에 사용
        for (int num : multiOf4) {
            System.out.println(num);
        }
```
### 중첩 루프
```java
		String[][] quotesInLangs = {
                {
                    "I am vengeance.",
                    "I am night.",
                    "I am Batman.",
                },
                {
                    "나는 복수를 하지.",
                    "나는 밤이지.",
                    "나는 배트맨이지.",
                },
        };

        String result = "";
        for (String[] quotes : quotesInLangs) {
            for (String quote : quotes) {
                result += quote + " "; // 🔴
            }
            result = result.trim().concat("\n");
        }

        System.out.println(result);
```
### continue/break
```java
		for (int i = 0; i < 100; i++) {

            //  💡 continue : 한 루프만 건너뜀
            if (i % 3 == 0) continue;

            //  💡 break : 반복 전체를 종료
            if (i == 10) break;

            System.out.println(i);
        }
```
#### label
```java
		//  💡 label : 중첩 루프에서 어느쪽을 continue, break 할 지 구분
        outer:
        for (int i = 0; i < 10; i++) {

            inner:
            for (int j = 0; j < 10; j++) {
                if (j % 2 == 0) continue inner;
                if (i * j >= 30) continue outer;

                if (j > 8) break inner;
                if (i - j > 7) break outer;

                System.out.printf("i: %d, j: %d%n", i, j);
            }
        }
```
### while
```java
		int i = 0;

        //  💡 while 문의 괄호에는 종료조건만
        while (i < 10) {
            // 종료조건 충족을 위한 값 변화는 외적으로 
            System.out.println(i++);
				}
```
#### do/while
- `do` 일단 수행하고 조건을 봄
```java
		int enemies = 0;

        System.out.println("일단 사격");

        do {
            System.out.println("탕");
            if (enemies > 0) enemies--;
        } while (enemies > 0);

        System.out.println("사격중지 아군이다");
```
