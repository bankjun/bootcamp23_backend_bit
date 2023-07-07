# JDBC(Java Database Connectivity)
자바를 이용한 데이터베이스 접속과 SQL 문장의 실행, 

그리고 실행결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 대한 규약

자바에서 만든 라이브러리 
Connection c = new ______().get _____  -> mysql or oracle etc.

이런식으로 사용할 수 있게 자바에서 인터페이스를 만들었고 이걸 가지고 mysql oracle등에서 구현해놓음

우리는 이걸 사용하면 되는것

new도 안한대 -> DriverManager가 있대 그 클래스 이름들을 알아야함

정해진 틀이 있음
