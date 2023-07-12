목차
[기초상식](#기초-상식)
[JSP/Servlet](#JSP-/-Servlet)
[MVC](#MVC)

# Web Programming

### 기초 상식
#### HTTP -> Hyper Text Transfer Protocol
#### HTML -> Hyper Text Markup Language
Markup Language - Markup tag를 사용하는 언어 <> </>

클라이언트 = 브라우저 <-> 서버 = 웹서버

* 역할1: HTTP에서 웹서버에 요청하면 웹서버의 디스크에있는 문서(HTML)를 내보내준다
  
* 역할2: HTTP에서 웹서버에 데이터를 요청하면 웹서버의 데이터베이스에 있는 데이터를 (프로그램으로)문서HTML로 변환하여 보내준다.
  -> 동적인 문서

자바에서 만든 웹서버 = WAS -> WAS를 통해서 통신하는 클래스 = servlet/JSP(추상클래스)


### 인터넷(네트워크 통신)의 이해
인터넷 != WWW(World Wide Web)

internet = 네트워크들의 연결, 서로 데이터를 주고 받기 위함, 한 컴퓨터의 자원이 한정되어있기 때문

네트워킹을 하기위해 필요한 것이 Protocol(= 네트워크 통신을 위한 규약)

INTERNET = TCP/IP 헤더를 사용하는 패킷으로 전 세계에서 사용되는 것, Socket

Web = 

그래서 우리가 해야할건 WAS, TOMCAT, 

### HTTP

### URL

인터넷 상의 자원위치

### 정적 웹 페이지
### 동적 웹 페이지

정적 VS 동적 비교

------------------
# JSP / Servlet

### JSP(Java Server Page)

* HTML페이지와 비슷하고 부분적으로 ```<% %>``` tag를 사용해서 Java코드를 작성한다.
* request객체를 사용할 수 있다.
* 파라메터들은 문자열로 반환된다.
* JSP는 실행전 Servlet으로 바뀐다.


### Servlet

* Servlet 클래스의 일반적 구조 -> 이클립스가 알아서 만들어줌
```java
public class HelloServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
  // HttpServlet 클래스의 doGet, doPost메소드를 제정의함
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
     // Post방식을 사용하는 모든 HTTP요청을 처리
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doGet(request, response);
	}
    // Get방식을 사용하는 모든 HTTP요청을 처리
}
```
* doGet, doPost메소드는 웹서버가 전달한 두객체를 인자로 받음.
  1) HttpServletRequest객체(request객체) -> 요청객체
  2) HttpServletResponse객체(response객체) -> 답변객체

이 객체들 안에 파라메터를 저장해서 전달하고 사용할 수 있음  

* 서블릿 호출시 GET 방식과 POST방식의 차이
  * GET방식 = URL과 파라미터 값들이 브라우저 주소창에 나타남
    * GET방식을 사용하는 경우: 빠르게 데이터를 보낼때, 4KB이하일때, 파라메터가 URL에 포함되어도될때 

  * POST방식 = 파라미터값들이 브라우저 주소창에 나타나지 않음
    * POST방식을 사용하는 경우: 4KB넘을때, URL에 파라메터가 붙으면안될때

 좀 더 보안을 유지하는 방법은 <form> tag 안에 
```html
 <input type="hidden" name="a" value="파라메터값"> 을 사용하면 된다.
```
 " a = 파라메터값" 으로 request객체 속에 저장되어 request되고 이를 servlet에서 ```request.getParameter("a")```로 받을 수 있음

-------------
# MVC
*책추천: 엔터프라이즈 애플리케이션 아키텍처 패턴 -> 이론서*

*스프링 인 엑션 -> 활용서*

### 3Layer Architecture & MVC Pattern

* 3layer -> presentation / service / DAO(repository)
  * presentation: 표현계층(controller request(요청제어), View(화면)), 사용자와 맞닿는 부분, 한가지만 부름, Main같은거? 
  
  * service: 핵심 비즈니스, 여러 기능을 수행해야 할 때 사용됨, 생략될 수 있음
  
  * DAO: Model=Data=BusiniessLogic
 
* MVC -> JSP(View) + Servlet(Controller) = Model 2
  *  JSP만 사용한거, JSP안에서 View,Controller다 만듦 =  Model 1

* JSP는 /WEB_INF/views/에 저장 -> 직접 접근할 일 없기때문

* 이때 Servlet(Controller)에서 view와 request,response 를 처리하게 된다.

* servlet에서 다른 veiw(JSP)를 연결해 주는경우, 제어를 넘겨주는 경우 **forward, Dispatch**
  ```java
    RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/views/deleteform.jsp"); // 
		rd.forward(request, response);
  ```

* 비즈니스만 처리하고 HTML을 반환할 필요가 없는 경우 **Redirect**를 사용하여 Default 페이지를 반환해준다.
  ```java
    response.sendRedirect("/defualtURL");
  ```
  
