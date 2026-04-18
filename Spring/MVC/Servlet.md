# 서블릿
## Hello 서블릿
> 서블릿은 톰캣 같은 웹 애플리케이션 서버를 직접 설치하고 그 위에 서블릿 코드를 클래스 파일로 빌드해서 올린 다음, 톰캣 서버를 실행하면 됨. 하지만 과정이 매우 번거로움
> 스프링 부트는 톰캣 서버를 내장하고 있으므로, 톰캣 서버 설치 없이 편리하게 서블릿 코드를 실행할 수 있다.
### 스프링 부트 서블릿 환경 구성
- `@ServletComponentScan`
- 스프링 부트는 서블릿을 직접 등록해서 사용할 수 있도록 애노테이션 지원
```java
@ServletComponentScan  
@SpringBootApplication  
public class ServletApplication {  
  
    public static void main(String[] args) {  
       SpringApplication.run(ServletApplication.class, args);  
    }  
  
}
```
- `@WebServlet` 서블릿 애노테이션
	- name: 서블릿 이름
	- urlPatterns: URL 매핑
- HTTP 요청을 통해 매핑된 URL이 호출되면 서블릿 컨테이너는 다음 메서드를 실행함
- `protected void service(HttpServletRequest request, HttpServletResponse response)`
```java
@WebServlet(name = "helloServlet", urlPatterns = "/hello")  
public class HelloServlet extends HttpServlet {  
    @Override  
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {  
//        super.service(req, resp);  
        System.out.println("HelloServlet.service");  
        System.out.println("request = " + request);  
        System.out.println("response = " + response);  
  
        String username = request.getParameter("username");  
        System.out.println("username = " + username);  
  
        response.setContentType("text/plain");  
        response.setCharacterEncoding("utf-8");  
        response.getWriter().write("hello " + username);  
    }  
}
```
### HTTP 요청 메시지 로그로 확인하기
- `application.properties`
```properties
logging.level.org.apache.coyote.http11=trace
```
- 서버가 받은 HTTP 요청 메시지 출력
> 참고: 운영서버에 이렇게 모든 요청 정보를 다 남기면 성능저하가 발생 가능. 개발 단계에만 적용
### 서블릿 컨테이너 동작 방식 설명
- 내장 톰캣 서버 생성
![](../../img/260418_28.png)
- HTTP 요청, HTTP 응답 메시지
![](../../img/260418_29.png)
- 웹 애플리케이션 서버의 요청 응답 구조
![](../../img/260418_30.png)
>참고: HTTP 응답에서 Content-Length는 웹 애플리케이션 서버가 자동으로 생성해줌
### welcome 페이지 추가
- webapp경로에 index.html 추가
## HttpServletRequest - 개요
- **역할**
	- HTTP 요청 메시지를 개발자가 직접 파싱해서 사용해도 되지만, 매우 불편함
	- 서블릿은 개발자가 HTTP 요청 메시지를 편리하게 사용할 수 있도록 대신에 HTTP 요청 메시지를 파싱
	- 그리고 그 결과를 `HttpServletRequest` 객체에 담아서 제공함
- HttpServletRequest를 사용하면 다음과 같은 HTTP 요청 메시지를 편리하게 조회할 수 있다.
- **HTTP 요청 메시지**
```
POST /save HTTP/1.1

Host: localhost:8080

Content-Type: application/x-www-form-urlencoded

username=kim&age=20
```
- START LINE
	- HTTP 메소드
	- URL쿼리 스트링
	- 스키마, 프로토콜
- 헤더
	- 헤더 조회
- 바디
	- form 파라미터 형식 조회
	- message body 데이터 직접 조회
- HttpServletRequest 객체는 추가로 여러가지 부가기능도 함께 제공
- **임시 저장소 기능**
- 해당 HTTP 요청이 시작부터 끝날 때까지 유지되는 임시 저장소 기능
	- 저장: `request.setAttribute(name, value)`
	- 조회: `request.getAttribute(name)`
- 세션 관리 기능: `request.getSession(create: true)`
## 