# JDBC(Java Database Connectivity)
자바를 이용한 데이터베이스 접속과 SQL 문장의 실행, 

그리고 실행결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 대한 규약

자바에서 만든 라이브러리 
```java
Connection c = Class.forName("드라이버? 클래스 이름")
```
이런식으로 사용할 수 있게 자바에서 인터페이스를 만들었고 이걸 가지고 mysql oracle등에서 구현해놓음

우리는 이걸 사용하면 되는것

정해진 틀이 있음(상투적인 코드), new도 안함 -> DriverManager가 있음 그 클래스 이름들을 알아야함

### 순서(바인딩 없을 때) (ex: InsertTest01.java)

> **1. 드라이브 매니저로부터 커넥션 객체를 얻어온다** -> 클래스 로딩, new가 아니라 for.Name을 통해서 직접 클래스를 로딩함
> ```JAVA
> Class.forName("org.mariadb.jdbc.Driver");
> ```
> 
> **2. 연결하기** -> 드라이버가 커넥션 객체를 생성하여 던져줌, URL을 드라이버매니저 한테 주고 그 커넥션을 얻어와 연결이 됨?
> ```JAVA
> String url = "jdbc:mariadb://192.168.0.150:3306/webdb?charset=utf8";
> conn = DriverManager.getConnection(url, "webdb", "webdb");
> ```
> 
> **3. Statement 생성** -> 커넥션을 통해 전달될 SQL문을 저장할 변수
> ```java
> stmt = conn.createStatement();
> ```
> 
> **4. SQL문(statement) 실행**
> ```java
> String sql = "insert into dept values(null, '" +deptName+"')";
> int count = stmt.executeUpdate(sql);
> ```
>
> **5. 결과처리**

-> insertTest01와 selectTest01 주석 참고


SQL + Parameter = 바인딩
-------
* "+"연산자를 사용하면 안되는 이유: 치환되는 방식이기 때문에 보안에 취약함, 아이디를 SQL문의 일부로 만들수 있게됨

-> 그래서 **PREPARE STATEMENTS** 사용

### PREPARE STATEMENTS

-> SQL을 실행할 준비만 시키고 

-> 바인딩: 메소드를 통해 입력된 값을 값 그자체로(ex: " **'123'** ") 들어가기 때문에 그 값이 SQL의 일부가 될 수 없음

-> 

원래 STATEMENTS: 
