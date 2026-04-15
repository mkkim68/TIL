# 의존관계 자동 주입
## 다양한 의존관계 주입 방법
- 생성자 주입
- 수정자 주입
- 필드 주입
- 일반 메서드 주입
### 생성자 주입
- 생성자를 통해 의존 관계 주입
- 특징
	- 생성자 호출시점에 딱 1번만 호출되는 것 보장
	- **불변, 필수** 의존관계에 사용
- *중요! 생성자가 딱 1개만 있으면 @Autowired를 생략해도 자동 주입 된다.* - 스프링 빈에만 해당
### 수정자 주입(setter 주입)
- setter라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서 의존관계 주입하는 방법
- 특징
	- **선택, 변경** 가능성이 있는 의존관계에 사용
	- 자바빈 프로퍼티 규약의 수정자 메서드 방식을 사용하는 방법
```java
@Component  
public class OrderServiceImpl implements OrderService {  
  
    private MemberRepository memberRepository;  
    private DiscountPolicy discountPolicy;  
  
    @Autowired  
    public void setMemberRepository(MemberRepository memberRepository) {  
        this.memberRepository = memberRepository;  
    }  
      
    @Autowired  
    public void setDiscountPolicy(DiscountPolicy discountPolicy) {  
        this.discountPolicy = discountPolicy;  
    }
    
    // ...
}
```
### 필드 주입
- 필드에 바로 주입하는 방법
 - 특징
	 - 코드가 간결해서 많은 개발자들을 유혹하지만 외부에서 변경이 불가능해서 테스트 하기 힘들다는 치명적 단점 존재
	 - DI 프레임워크가 없으면 아무것도 할 수 없다
	 - 사용하지 말자!
		 - 애플리케이션의 실제 코드와 관계 없는 테스트 코드
		 - 스프링 설정을 목적으로 하는 @Configuration 같은 곳에서만 특별한 용도로 사용
```java
@Component  
public class OrderServiceImpl implements OrderService {  
  
    @Autowired
    private MemberRepository memberRepository;  
    @Autowired 
    private DiscountPolicy discountPolicy;
    
    // ...
}
```
### 일반 메서드 주입
- 일반 메서드를 통해 주입받을 수 있다
- 특징
	- 한번에 여러 필드를 주입 받을 수 있음
	- 일반적으로 잘 사용 안함
```java
@Component  
public class OrderServiceImpl implements OrderService {  
  
    private MemberRepository memberRepository;  
    private DiscountPolicy discountPolicy;  

    @Autowired  
    public void init(MemberRepository memberRepository, DiscountPolicy discountPolicy) {  
        this.memberRepository = memberRepository;  
        this.discountPolicy = discountPolicy;   
    }
    //
}
```
## 옵션 처리
- 주입할 스프링 빈이 없어도 동작해야 할 때가 있다
- 그런데 `@Autowired`만 사용하면 `required` 옵션의 기본값이 `true`로 되어 있어서 자동 주입 대상이 없으면 오류가 발생함
- 자동 주입 대상을 옵션으로 처리하는 방법
	- `@Autowired(required=false)`: 자동 주입할 대상이 없으면 수정자 메서드 자체가 호출 안됨
	- `org.springframework.lang.@Nullable`: 자동 주입할 대상이 없으면 null이 입력됨
	- `Optional<>`: 자동 주입할 대상이 없으면 `Optional.empty`가 입력됨
```java
public class AutowiredTest {  
  
    @Test  
    void AutoWiredOption() {  
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(TestBean.class);  
    }  
  
    @Component  
    static class TestBean {  
  
        @Autowired(required = false)  
        public void setNoBean1(Member noBean1) {  
            System.out.println("noBean1 = " + noBean1);  
        }  
  
        @Autowired  
        public void setNoBean2(@Nullable Member noBean2) {  
            System.out.println("noBean2 = " + noBean2);  
        }  
  
        @Autowired  
        public void setNoBean3(Optional<Member> noBean3) {  
            System.out.println("noBean3 = " + noBean3);  
        }  
    }  
}
```
## 생성자 주입을 선택해라
- 과거에는 수정자 주입과 필드 주입을 많이 사용했지만, 최근에는 스프링을 포함한 DI 프레임워크 대부분이 생성자 주입을 권장함. 그 이유는 다음과 같음
### 불변
- 대부분의 의존관계 주입은 한번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없음. 오히려 대부분의 의존관계는 애플리케이션 종료 전까지 변하면 안됨
- 수정자 주입을 사용하면 setXxx 메서드를 public으로 열어두어야 함
- 누군가 실수로 변경할 수도 있고, 변경하면 안되는 메서드를 열어두는 것은 좋은 설계 방법이 아니다
- 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출되는 일이 없다. 따라서 불변하게 설계할 수 있음
### 누락
- 프레임워크 없이 순수한 자바 코드를 단위 테스트 하는 경우에 다음과 같이 수정자 의존관계인 경우
```java
@Test  
void createOrder() {  
    OrderServiceImpl orderService = new OrderServiceImpl();  
    orderService.createOrder(1L, "itemA", 10000);  
}
```
- 이렇게 하면 주입 데이터를 누락했을 때 "컴파일 오류"가 발생함
- IDE에서 바로 어떤 값을 필수로 주입해야 하는지 알 수 있음
### final 키워드
- 생성자 주입을 사용하면 필드에 `final` 키워드를 사용할 수 있다. 그래서 생성자에서 혹시라도 값이 설정되지 않는 오류를 컴파일 시점에 막아줌
```java
    private final MemberRepository memberRepository;  
    private final DiscountPolicy discountPolicy;  
  
    public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) { 
        this.memberRepository = memberRepository;  
    }
```
- 필수 필드인 `discountPolicy`에 값이 설정되지 않았음. 이 부분이 누락되었다는 것을 컴파일 오류로 알려준다
- `java: variable discountPolicy might not have been initialized`
- *컴파일 오류는 세상에서 가장 빠르고 좋은 오류다!*
> 참고: 수정자 주입을 포함한 나머지 주입 방식은 모두 생성자 이후에 호출되므로, 필드에 `final` 키워드를 사용할 수 없다. 오직 생성자 주입 방식만 `final` 키워드 사용 가능
## 롬복과 최신 트렌드
- 막상 개발을 해보면 대부분이 다 불변이고, 그래서 다음과 같이 생성자에 final 키워드를 사용하게 됨
- 그런데 생성자도 만들어야 하고, 주입 받은 값을 대입하는 코드도 만들어야 하고...
- 필드 주입처럼 좀 편리하게 사용하는 방법은 없을까?
- 롬복 적용 코드
```java
@Component  
@RequiredArgsConstructor  
public class OrderServiceImpl implements OrderService {  
  
    private final MemberRepository memberRepository;  
    private final DiscountPolicy discountPolicy;  

}
```
- Lombok 라이브러리가 제공하는 `@RequiredArgsConstructor` 기능을 사용하면 `final`이 붙은 필드를 모아서 생성자를 자동으로 만들어준다. (코드에는 보이지 않지만 실제 호출 가능)
## 조회 빈이 2개 이상 - 문제
```java
public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {  
    this.memberRepository = memberRepository;  
    this.discountPolicy = discountPolicy;  
}
```
- 이 때 `@Component`로 `FixDiscountPolicy`, `RateDiscountPolicy` 둘 다 스프링 빈으로 등록했기 때문에 컴파일 에러 발생
	- `NoUniqueBeanDefinitionException`
- 이 때 하위 타입으로 지정할 수도 있지만 하위 타입으로 지정하는 것은 DIP를 위배하고 유연성이 떨어짐
- 그리고 이름만 다르고 완전히 똑같은 타입의 스프링 빈이 2개 있을 떄 해결이 안됨
- 스프링 빈을 수동 등록해서 문제를 해결해도 되지만, 의존 관계 자동 주입에서 해결하는 여러 방법이 있다.
## @Autowired 필드 명, @Qualifier, @Primary
- 조회 대상 빈이 2개 이상일 때 해결 방법
	- @Autowired 필드 명 매칭
	- @Qualifier -> @Qualifier끼리 매칭 -> 빈 이름 매칭
	- @Primary 사용
### @Autowired 필드 명 매칭
- `@Autowired`는 타입 매칭을 시도하고 이 때 여러 빈이 있으면 필드 이름, 파라미터 이름으로 빈 이름을 추가 매칭함
```java
@Autowired
private DiscountPolicy rateDiscountPolicy;
```
1. 타입 매칭
2. 타입 매칭의 결과가 2개 이상일 때 필드 명으로 빈 이름 매칭
### @Qualifier 사용
```java
@Component  
@Qualifier("mainDiscountPolicy")  
public class RateDiscountPolicy implements DiscountPolicy{/*... */}
```
```java
public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {  
    this.memberRepository = memberRepository;  
    this.discountPolicy = discountPolicy;  
}
```
- 만약 `@Qualifier("mainDiscountPolicy")`를 못찾는다면?
	- `mainDiscountPolicy`라는 이름의 스프링 빈을 추가로 찾는다
	- 하지만 `@Qualifier`는 `@Qualifier`를 찾는 용도로만 사용하는게 명확하고 좋음
### @Primary 사용
- 우선순위를 정하는 방법
- 여러 빈 매칭되면 @Primary가 우선권 가짐
```java
@Component  
@Primary  
public class RateDiscountPolicy implements DiscountPolicy{ /* ... */ }
```
## 애노테이션 직접 만들기
- `@Qualifier("mainDiscountPolicy")` 이렇게 문자를 적으면 컴파일시 타입 체크가 안됨. 다음과 같은 애노테이션을 만들어서 문제 해결 가능
```java
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})  
@Retention(RetentionPolicy.RUNTIME)  
@Inherited  
@Documented  
@Qualifier("mainDiscountPolicy")  
public @interface MainDiscountPolicy {  
}
```
```java
@Component  
@MainDiscountPolicy  
public class RateDiscountPolicy implements DiscountPolicy{ }
```
```java
public OrderServiceImpl(MemberRepository memberRepository, @MainDiscountPolicy DiscountPolicy discountPolicy) {  
    this.memberRepository = memberRepository;  
    this.discountPolicy = discountPolicy;  
}
```
- 애노테이션에는 상속이란 개념이 없다.
- 이렇게 여러 애노테이션을 모아서 사용하는 기능은 스프링이 지원해주는 기능
- 다른 애노테이션도 함께 조합해서 사용 가능
## 조회한 빈이 모두 필요할 때, List, Map
- 의도적으로 정말 해당 타입의 스프링 빈이 다 필요한 경우도 있음
```java
public class AllBeanTest {  
  
    @Test  
    void findAllBean() {  
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(AutoAppConfig.class, DiscountService.class);  
  
        DiscountService discountService = ac.getBean(DiscountService.class);  
        Member member = new Member(1L, "userA", Grade.VIP);  
        int discountPrice = discountService.discount(member, 10000, "fixDiscountPolicy");  
  
        Assertions.assertInstanceOf(DiscountService.class, discountService);  
        Assertions.assertEquals(1000, discountPrice);  
  
        int rateDiscountPrice = discountService.discount(member, 20000, "rateDiscountPolicy");  
        Assertions.assertEquals(2000, rateDiscountPrice);  
    }  
  
    @Component  
    static class DiscountService {  
        private final Map<String, DiscountPolicy> policyMap;  
        private final List<DiscountPolicy> policies;  
  
        @Autowired  
        public DiscountService(Map<String, DiscountPolicy> policyMap, List<DiscountPolicy> policies) {  
            this.policyMap = policyMap;  
            this.policies = policies;  
  
            System.out.println("policyMap = " + policyMap);  
            System.out.println("policies = " + policies);  
        }  
  
        public int discount(Member member, int price, String discountCode) {  
            DiscountPolicy discountPolicy = policyMap.get(discountCode);  
            return discountPolicy.discount(member, price);  
        }  
    }  
}
```
#### 로직 분석
- DiscountService는 Map으로 모든 `DiscountPolicy`를 주입받음
- `discount()` 메서드는 discountCode로 `fixDiscountPolicy`가 넘어오면 map에서 `fixDiscountPolicy` 스프링 빈을 찾아서 실행. 물론 `rateDiscountPolicy`가 넘어오면 `rateDiscountPolicy` 스프링 빈을 찾아 실행
#### 주입 분석
- `Map<String, DiscountPolicy>`: map의 키에 스프링 빈의 이름을 넣어주고 그 값으로 `DiscountPolicy` 타입으로 조회한 모든 스프링 빈을 담아준다.
- `List<DiscountPolicy>`: `DiscountPolicy` 타입으로 조회한 모든 스프링 빈을 담아준다.
- 만약 해당하는 탕딥의 스프링 빈이 없으면 빈 컬렉션이나 Map을 주입함
## 자동, 수동의 올바른 실무 운영 기준

> 편리한 자동 기능을 기본으로 사용하자
- 수동은 너무 번거로움
- 자동 빈 등록을 사용해도 OCP, DIP 지킬 수 있음
### 그렇다면 수동 빈은 언제 사용하면 좋을까?
- **업무 로직 빈**: 웹을 지원하는 컨트롤러, 핵심 비즈니스 로직이 있는 서비스, 데이터 계층의 로직을 처리하는 리포지토리 등이 모두 업무 로직임. 보통 비즈니스 요구사항을 개발할 때 추가되거나 변경됨
- **기술 지원 빈**: 기술적인 문제나 공통 관심사(AOP)를 처리할 때 주로 사용. 데이터베이스 연결이나 공통 로그 처리 처럼 업무 로직을 지원하기 위한 하부 기술이나 공통 기술들
- 다형성을 적극 활용하는 비즈니스 로직은 수동 등록을 고려해 보자