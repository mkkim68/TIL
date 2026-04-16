# 빈 생명주기 콜백
## 빈 생명주기 콜백 시작
- 데이터베이스 커넥션 풀이나, 네트워크 소켓처럼 애플리케이션 시작 시점에 필요한 연결을 미리 해두고, 애플리케이션 종료 시점에 연결을 모두 종류하는 작업을 진행하려면, 객체의 초기화와 종료 작업이 필요하다.
- `NetworkClient`는 애플리케이션 시작 시점에 `connect()`를 호출해서 연결을 맺어두어야 하고 애플리케이션 종료 시 `disConnect()` 호출해서 연결을 끊어야 함
```java
// NetworkClient.java
package hello.core.lifecycle;  
  
public class NetworkClient {  
  
    private String url;  
  
    public NetworkClient() {  
        System.out.println("생성자 호출, url = " + url);  
        connect();  
        call("초기화 연결 메시지");  
    }  
  
    public void setUrl(String url) {  
        this.url = url;  
    }  
  
    // 서비스 시작시 호출  
    public void connect() {  
        System.out.println("connect: " + url);  
    }  
  
    public void call(String message) {  
        System.out.println("call: " + url + "message = " + message);  
    }  
  
    // 서비스 종료시 호출  
    public void disconnect() {  
        System.out.println("close " + url);  
    }  
}

// BeanLifeCycleTest.java
package hello.core.lifecycle;  
  
import org.junit.jupiter.api.Test;  
import org.springframework.context.ConfigurableApplicationContext;  
import org.springframework.context.annotation.AnnotationConfigApplicationContext;  
import org.springframework.context.annotation.Bean;  
import org.springframework.context.annotation.Configuration;  
  
public class BeanLifeCycleTest {  
  
    @Test  
    public void lifeCycleTest() {  
        ConfigurableApplicationContext ac = new AnnotationConfigApplicationContext(LifeCycleConfig.class);  
        NetworkClient client = ac.getBean(NetworkClient.class);  
        ac.close();  
  
    }  
  
    @Configuration  
    static class LifeCycleConfig {  
  
        @Bean  
        public NetworkClient networkClient() {  
            NetworkClient networkClient = new NetworkClient();  
            networkClient.setUrl("http://hello-spring.dev");  
            return networkClient;  
        }  
    }  
}
```
- 하지만 url이 null값으로 들어감
	- 객체 생성 단계에 url이 없고 외부에서 수정자 주입을 통해서 `setUrl()`이 호출되어야 url이 존재하게 되기 때문
- 스프링 빈은 간단하게 다음과 같은 라이프사이클을 가진다
	- **객체 생성 -> 의존관계 주입**
- **스프링은 의존관계 주입이 완료되면 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능을 제공**한다. 또한 **스프링은 스프링 컨테이너가 종료되기 직전에 소멸 콜백을 준다**. 따라서 안전하게 종료 작업 진행 가능
### 스프링 빈의 이벤트 라이프사이클
1. 스프링 컨테이너 생성
2. 스프링 빈 생성
3. 의존관계 주입
4. 초기화 콜백
5. 사용
6. 소멸전 콜백
7. 스프링 종료
- 초기화 콜백: 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출
- 소멸전 콜백: 빈이 소멸되기 직전에 호출
> 참고: 객체의 생성과 초기화를 분리하자
## 인터페이스 InitializingBean, DisposableBean
```java
package hello.core.lifecycle;  
  
import org.springframework.beans.factory.DisposableBean;  
import org.springframework.beans.factory.InitializingBean;  
  
public class NetworkClient implements InitializingBean, DisposableBean {  
  
    private String url;  
  
    public NetworkClient() {  
        System.out.println("생성자 호출, url = " + url);  
    }  
  
    public void setUrl(String url) {  
        this.url = url;  
    }  
  
    // 서비스 시작시 호출  
    public void connect() {  
        System.out.println("connect: " + url);  
    }  
  
    public void call(String message) {  
        System.out.println("call: " + url + "message = " + message);  
    }  
  
    // 서비스 종료시 호출  
    public void disconnect() {  
        System.out.println("close " + url);  
    }  
  
    @Override  
    public void afterPropertiesSet() throws Exception {  
        System.out.println("NetworkClient.afterPropertiesSet");  
  
        connect();  
        call("초기화 연결 메시지");  
    }  
  
    @Override  
    public void destroy() throws Exception {  
        System.out.println("NetworkClient.destroy");  
        disconnect();  
    }  
}
```
```text
생성자 호출, url = null
NetworkClient.afterPropertiesSet
connect: http://hello-spring.dev
call: http://hello-spring.devmessage = 초기화 연결 메시지
NetworkClient.destroy
close http://hello-spring.dev
```
- 출력 결과를 보면 초기화 메서드가 주입 완료 후에 적절하게 호출 된 것을 확인 가능
- 스프링 컨테이너의 종료가 호출되자 소멸 메서드가 호출 된 것도 확인 가능
### 초기화, 소멸 인터페이스 단점
- 이 인터페이스는 스프링 전용 인터페이스다. 해당 코드가 스프링 전용 인터페이스에 의존함
- 초기화, 소멸 메서드의 이름 변경 불가
- 내가 코드를 고칠 수 없는 외부 라이브러리에 적용할 수 없음
> 참고: 인터페이스를 사용하는 초기화, 종료 방법은 스프링 초창기에 나온 방법. 지금은 다음의 더 나은 방법들 덕분에 사용 X
## 빈 등록 초기화, 소멸 메서드
- 설정 정보에 `@Bean(initMethod="init, destroyMethod = "close")`처럼 초기화, 소멸 메서드를 지정할 수 있다.
```java
// NetworkClient.java

public class NetworkClient{  
  // ...
  
    public void init() {  
        System.out.println("NetworkClient.afterPropertiesSet");  
  
        connect();  
        call("초기화 연결 메시지");  
    }  
  
    public void close() {  
        System.out.println("NetworkClient.destroy");  
        disconnect();  
    }  
}

// BeanLifeCycleTest.java
public class BeanLifeCycleTest {    
  // ...
  
    @Configuration  
    static class LifeCycleConfig {  
  
        @Bean(initMethod = "init", destroyMethod = "close")  
        public NetworkClient networkClient() {  
            NetworkClient networkClient = new NetworkClient();  
            networkClient.setUrl("http://hello-spring.dev");  
            return networkClient;  
        }  
    }  
}
```
- 출력 결과
```Text
생성자 호출, url = null
NetworkClient.afterPropertiesSet
connect: http://hello-spring.dev
call: http://hello-spring.devmessage = 초기화 연결 메시지
NetworkClient.destroy
close http://hello-spring.dev
```
### 설정 정보 사용 특징
 - 메서드 이름을 자유롭게 줄 수 있다
 - 스프링 빈이 스프링 코드에 의존 X
 - 코드가 아니라 설정 정보를 사용하기 때문에 코드를 고칠 수 없는 외부 라이브러리에도 초기화, 종료 메서드 적용 가능
### 종료 메서드 추론
- `@Bean`의 `destroyMethod`에는 특별한 기능 존재
- 라이브러리는 대부분 `close`, `shutdown` 이라는 이름의 종료 메서드 사용
- `@Bean`의 `destroyMethod`는 기본값이 `(inferred)`(추론)으로 등록되어있음
- 이 추론 기능은 `close`, `shutdown`이라는 이름의 메서드를 자동으로 추론해서 호출해줌.
- 따라서 직접 적어주지 않아도 잘 동작함
- 추론 기능을 사용하기 싫으면 `destroyMethod=""`처럼 빈 공백 지정
## 애노테이션 @PostConstruct, @PreDestroy
```java
@PostConstruct  
public void init() {  
    System.out.println("NetworkClient.afterPropertiesSet");  
  
    connect();  
    call("초기화 연결 메시지");  
}  
  
@PreDestroy  
public void close() {  
    System.out.println("NetworkClient.destroy");  
    disconnect();  
}
```
- 출력 결과
```text
생성자 호출, url = null
NetworkClient.afterPropertiesSet
connect: http://hello-spring.dev
call: http://hello-spring.devmessage = 초기화 연결 메시지
NetworkClient.destroy
close http://hello-spring.dev
```
- 두 애노테이션만 사용하면 가장 편리하게 초기화와 종료 실행 가능
### 특징
- 최신 스프링에서 가장 권장하는 방법
- 애노테이션 하나만 붙이면 되므로 매우 편리하다.
- 패키지를 잘 보면 javax. annotation.PostConstruct 이다. 스프링에 종속적인 기술이 아니라 JSR-250라는 자바 표준 이다. 따라서 스프링이 아닌 다른 컨테이너에서도 동작한다.
- 컴포넌트 스캔과 잘 어울린다.
- 유일한 단점은 외부 라이브러리에는 적용하지 못한다는 것이다. 외부 라이브러리를 초기화, 종료 해야 하면 @Bean의 기능을 사용하자.