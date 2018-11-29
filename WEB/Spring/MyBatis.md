# MyBatis

- Ibtis(2.xV) => MyBatis(3.xV)으로 바뀜

- 자바 오브젝트와 SQL문 사이의 자동 Mapping 기능을 지원하는 **ORM프레임워크**
- 객체와 SQL사이의 파라미터 Mapping작업을 자동으로 해줌

## MyBatis특징

1. 쉬운 접근성과 코드의 간결함
   - JDBC의 모든 기능을 대부분 제공
   - 코드의 약 70%가 줄어든다.
2. SQL문과 프로그래밍 코드의 분리
   - SQL에 변경이 있을 때마다 자바 코드를 수정하거나 컴파일 하지 않아도 된다.
3. 다양한 프로그래밍 언어로 구현가능
   - Java, C#, Ruby



### 설계

- sqlsession Template는 즉 sqlsession역할을 한다.

1. SqlSessionFactoryBuilder
   - 공장 설계
   - SqlSessionFactory를 만든다.
2. SqlSessionFacory
   - SqlSession을 만든다.
3. SqlSession
   - 모든 CRUD작업 담당
   - transation관리(Commit, rollback) - JDBC(Connection)

## MyBatis 설정

- ##### web사용X, 순수java만 사용할 경우의 **project 설정** (maven사용)

  new -> maven project -> next -> 프로젝트 이름 2개 작성(똑같이 해도됨) -> finish

- ##### 만든후 Build Path해줘야한다. 

  Build Path => jre 지우고 버전에 맞게 설정 => java compier에서 1.8로 변경

- ##### pom.xml 설정해줘야한다.

  ```xml
  <!-- oracle library 다운로드 위치 설정 -->
  <repositories>
  	<repository>
  		<id>codelds</id>
  		<url>https://code.lds.org/nexus/content/groups/main-repo</url>
  	</repository>
  </repositories>
  
  <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
  <!-- myBatis 설정을 위한 library -->
  <dependency>
  	<groupId>org.mybatis</groupId>
  	<artifactId>mybatis</artifactId>
  	<version>3.2.8</version>
  </dependency>
  
  <!-- 오라클 설치 -->
  <dependency>
  	<groupId>com.oracle</groupId>
  	<artifactId>ojdbc6</artifactId>
  	<version>11.2.0.3</version>
  	<scope>compile</scope>
  </dependency>
  
  <!-- https://mvnrepository.com/artifact/log4j/log4j -->
  <!-- myBatis는 콘솔에러가 보기 어렵기 때문에 log4j로 확인한다. -->
  <dependency>
  	<groupId>log4j</groupId>
  	<artifactId>log4j</artifactId>
  	<version>1.2.17</version>
  </dependency>
  ```
