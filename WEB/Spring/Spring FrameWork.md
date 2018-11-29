# Spring FrameWork

### eclipe에서 spring 설치(eclipe에 들어가서 시작)

- help => eclipe market눌러서 sts검색 => install누르기(spring) => Security warning이 뜨면 맨 왼쪽클릭

  => 계속 설치 => selectAll 설치 => restart => 끝

### spring 기본 project 만들기(web사이트 만드는것 x)

- new => other => spring검색 => Legacy Project => next => simple spring maven(templetes설정) => finish

#### project만든후 Build Path해줘야한다.

- project 우클릭 => buildPath => library => jre삭제 => Add library => jre 누르기 => java Compiler => 1.8로 변경 => yes누르기

#### pom.xml문서 변경

- java-version => 1.8로 변경
- spring-version => 4.3.11(4.3.10)으로 바꾸기
- depedencies에가서 맨위의 context 빼고 다 remove

<hr>

## 라이브러리와 프레임 워크의 차이점 - 많이 물어보는 질문

- 라이브러리
  - 유저코드가 라이브러리를 호출
  - 독립적을 작성
  - 유저코드가 제어
- 프레임 워크
  - 프레임워크코드가 유저코드를 호출
  - 프레임워크가 제어
  - 프레임워크 클래스를 서브클래싱해서 작성

### 메이븐

- 라이브러리 관리 + 빌드 툴

- 프로젝트에 필요한 관련된 라이브러리를 관리해주는 것

- 필요한 라이브러리를 다운받아 필요한 것만 build path 해주면 됨

- #### maven기반의 Project Pachage구조

  - src/main/java - 모든 자바소스
  - src/main/resources - 설정문서 모아두기
  - src/test/java - 단위테스트할때 사용

<hr>
- 생성 : <bean class=""> ->@Component

- 주입  -> @Autowired, @Resource

  ```xml
  <bean class=""> 
  	<constructor-arg>
  	<property>
  </bean>
  ```

## Spring Framework의 특징

- java개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크이다.

1. ##### Spring DI(Dependency InJection) = IoC(Inversion of Control)

   - container로 부터 의존관계에 있는 것을 자동으로 넣어주는 것
   - 객체들의 라이프사이클을 관리해준다. - container
   - 객체와 객체간의 **결합도를 최대한 낮춘다.**
     - 유지보수할때 소스 변경이 적다.
   - setter로서의 주입
   - 생성자로서의 주입
   - DI 컨테이너가 관리하는 객체를 빈이라고한다.
   - 컨테이너 빈 팩토리 -> 빈들을 관리함

2. ##### Spring AOP(Aspect Oriented Programing)

   - 관점 지향 프로그램(servlet에서 filter와 비슷)
   - 공통기능을 빼고 praxy server을 이용해서 wearving(위빙)해서 호출해서 쓴다.
   - 공통 기능과 핵심기능이 완전히 나뉘어져 있다.
   - 공통코드(advice)종류 5가지
     1. around : 사전, 사후처리(많이 사용)
     2. before : 사전 처리
     3. after : 예외가 발생하건, 제대로 돌아가던 사후처리 해줌
     4. after-throwing : 예외가 발생했을 때만 사후처리
     5. after-returning : 정상적으로 돌아갔을 때만 사후처리

3. ##### Spring Web MVC

4. ##### Spring ORM(Object Relation Mapping)->JDBC역할을 한다.

   - 객체 DB를 연결해주는 역할

5. ##### Spring Ajax

   - 화면의 새로고침 없이 화면을 갱신해준다.
   - 응답해주는 사이클이 jsp와 다르다.

6. ##### Spring  tranjection

7. ##### Spring tiles -> (view template)-jsp의 include와 비슷

   - 설정에 mapping시켜주면 된다.

8. ##### Spring Security

   - 인증(로그인)과 권한

9. ##### Spring POJO



## 사용자 관리 프로젝트 아키텍쳐

1. #### Presentation Layer(view, controller)

   - 브라우저상의 웹클라이언트의 요청, 응답 처리
   - controller에서 예외 처리
   - 비즈니스 로직과 최종 UI를 분리하기 위한 컨트롤러 제공

2. #### Service Layer(Service)

3. #### DataAccess Layer(DAO)

4. #### 도메인 모델 클래스(DTO, VO)

   - 3개의 계층 전체에 걸쳐 사용
   - private으로 선언된 멤버변수가 있어야하고,
   - 그 변수에 대한 getter와 setter메서드를 가진 클래스



<hr>

### Log4j

- java에서 빠르고 효과적으로 로깅할 수 있도록 도와주는 오픈소스



## spring maven기반의 web MVC

> MVC(Model-View-Controller)

### WebMVC project 만들기

- spring Legacy Project 설정 -> spring MVC선택 -> next -> 

  패키지명을 ex) aaa.mvc.controller 로 설정(파일을 3개 이상 해줘야한다.)  ->finish

- Build Path 해준다.

- webpage만들때는 project Facts에 java=1.8로 변경

- ~.xml문서를 공유해서 사용하려면 context param을 써야한다.

<hr>

src/main/java => controller, service, dao, dto ...
src/main/resources => mapper , config
src/main/test

src/main/webapp/ => root영역(Webcontent와 동일)
src/main/webapp/resource => css, js, img

src/main/webapp/WEB-INF/spring =>root-context.xml, spring-contex.xml
src/main/webapp/WEB-INF/views => ~.jsp문서
src/main/webapp/WEB-INF/ => web.xml문서



### post방식으로 넘어온 data 한글Encoding

- spring에서 제공해주는 코드를 web.xml문서에 작성해주면 된다.

  ```xml
  <filter>
  	<filter-name>characterEncoding</filter-name>
  	<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  	<init-param>
  		<param-name>encoding</param-name>
  		<param-value>UTF-8</param-value>
  	</init-param>
  </filter>
  
  <filter-mapping>
  	<filter-name>characterEncoding</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>
  		
  ```

<hr>

## Transaction

- 가장 큰 예시 : 계좌이체

- AOP기반으로 spring에서 transaction을 만들어 놓았다.

- 성공하면 commit해주고, 실패하면 rollback을 해준다.

- AOP와 transaction에 관련된 LIB가 필요하다.

- DB와 Java언어가 데이터를 주고 받는 과정에 원자성을 부여하는 수단

- ACID(4가지)

  - 원자성(Atomicity) : 전체가 하나로 묶여서 commit, rollback이 되는 것, 일부분만 되는 것은 X

  - 일관성(Consistency) : 일관성있게 모두 성공이면 성공,, 실패면 실패 이렇게 되야한다.

    					일부분만 되는것은 안된다.

  - 고립성(Isolation) : 서로 다른 트랜잭션이 동일한 데이터에 동시에 접근할 경우 알맞게 

    				동시접근제어를 해줘야한다.

  - 지속성(Durability) : 트랜잭션이 완료되면, 그 결과가 지속적으로 유지되어야한다.

    				   * 프로그램상에서 유지되고, 실제 DB에서도 유지되어야한다.

- Manager설정(JDBC사용) : DataSourceTransactionManager사용하면된다.

#### trasaction전파(propagation)

- REQUIRED
  - 메소드를 수행하는데 트랜잭션이 필요하다는 것을 의미
  - 현재 진행중인 트랜잭션이 존재하면 해당 트랜잭션을 사용
  - 존재하지 않다면 새로운 트랜잭션 생성
- MANDATORY
  - 메소드를 수행하는데 트랜잭션이 필요하다는 것을 의미
  - REQUERED와 달리 진행중이 트랜잭션이 존재하지 않는다면 Exception발생

#### transaction 격리(isolation)

- 동시에 여러 트랜잭션이 진행될 때에 트랜잭션의 작업 결과를 다른 트랜잭션에게 어떻게 노출할 것인지를 결정하는 기준

#### transaction <tx:method>태그의 속성

- name : 트랜잭션이 적용될 메소드이름 명시
- propagation : 트랜잭션 전파규칙을 설정(REQUIRED(기본값), MANDATORY, ...)
- isolation : 격리레벨을 설정(DEFAULT, READ_UNCOMMITTED...)
- read-only : 읽기전용여부 설정
- no-rollback-for : 롤백하지 않을 exception타입을 지정
- rollback-for : 롤백할 exception타입을 지정
- timeout : 트랜잭션 타입아웃 시간을 초단위로 지정



