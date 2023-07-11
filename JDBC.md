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
> ```
> boolean값, 실행결과 등을 처리해주는코드
> ```

-> insertTest01와 selectTest01 주석 참고


SQL + Parameter = 바인딩
-------
* "+"연산자를 사용하면 안되는 이유: 치환되는 방식이기 때문에 보안에 취약함, 아이디를 SQL문의 일부로 만들수 있게됨

-> 그래서 **PREPARE STATEMENTS** 사용

### PREPARE STATEMENTS
statement란, sql문을 실행하는 역할을 하는 클래스
-> SQL을 실행할 준비만 시키고

-> 바인딩: 메소드를 통해 입력된 값을 값 그자체로(ex: " **'123'** ") 들어가기 때문에 그 값이 SQL의 일부가 될 수 없음

-> SQLInjection 방지

-> 기존의 statement에서 진행하는 parse과정을 생략하여 성능을 향상시킴 [참조사이트]:https://jaehoney.tistory.com/179

### 바인딩을 사용했을 떄 순서(ex: InsertTest02)

> 0. 자원정리를 위해 try문 밖에 Connection, PreparedStatement객체 생성
>  ```java
>  Connection conn = null;
>	 PreparedStatement pstmt = null;
>  ```  
> 1. JDBC Driver Class 로딩
> ```java
> Class.forName("org.mariadb.jdbc.Driver");
> ```
> 2. 연결하기
> ```java
> String url = "jdbc:mariadb://192.168.0.150:3306/webdb?charset=utf8";
>	conn = DriverManager.getConnection(url, "webdb", "webdb"); // PreparedStatement conn = null 을 static변수로 선언, 자원정리를 위해
> ```
> 3. SQL문 생성(**prepare** statements) -> preparestatement가 보안성이 높음
> ```java
> String sql = "insert into dept values(null, ?)";
>	pstmt = conn.prepareStatement(sql);
> ```
> 4. 바인딩(binding)
> ```java
> pstmt.setString(1, deptName);
> ```
> 5. SQL 실행
> ```java
> int count = pstmt.executeUpdate(); <- 이제 여기에 sql문을 넣지 않음
> ```
> 6. 결과처리


# DAO(Data Access Object), VO
DB를 사용해 데이터를 조회하거나 조작하는 기능(CRUD)을 전담하도록 만든 오브젝트

DB에 CRUD하는 코드를 어플리케이션 자체에 작성하면 객체지향이 아니지 그니까 따로 DAO클래스로 빼 놓은거지 -> 역할분리

**VO:** 값들을 가지고 있는 클래스 (employee의 이름, 사번 등등 을 저장하고 set, get하는 클래스)

> 이름을 입력받아 해당 이름을 가진 레이블을 반환해주는 프로그램
> 패키지구성
> hr.dao -> EmployeeDao -> Vo를 가지고 DB에 CRUD하는 메소드들을 정의한 클래스
> hr.dao.test -> EmployeeDaoTest(테스트코드)
> 
> vo -> EmployeeVo -> 변수들에 접근하기 위한 getter, setter, toString 을 가지는 클래스
> 
> main -> Main -> DAO와 VO를 가지고 실질적으로 실행하는 클래스
