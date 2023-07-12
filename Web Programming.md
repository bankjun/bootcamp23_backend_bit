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

---------
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


### Servlet

* Servlet 클래스의 일반적 구조


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
