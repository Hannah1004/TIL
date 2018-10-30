# JSP&Servlet

jdk설치 + tomcat설치 + 개발 tool(eclipse) + 브라우저(chrom)

### Tomcat의 역할

1. web Server

   - 사용자의 요청이 들어오면

     => ~.jsp문서를 읽어서 정적코드(html, css, js, img)와 동적코드(java코드) 분리

   - 동적코드를 WAS에게 전송

   - WAS가 보내준 실행결과와 정적코드를 합쳐서 브라우저에 응답(response)

2.  web Application Server = WAS

   - 동적코드를 파싱(컴파일)
   - ~.java에 해당하는 servlet문서를 생성  -> .class생성
   - 최종결과를 html로 변환해서 webServer에게 전송!

<hr>

- jsp가 실행되는 곳
  - C:\Edu\webWorkSpace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps

- class가 모여있는 곳(서버가 실행할때 만들어준다.java, class파일)- was가 만듬
  - C:\Edu\webWorkSpace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\work\Catalina\localhost\step03_JspExam\org\apache\jsp

<hr>

## JSP 스크립팅요소

1. <%  %>  :  기본 java코드 작성 (스크립트릿요소)
2. <%=  %>  : 출력문
3. <%!  %> :  선언문(전역변수 or 메소드 선언)
4. <%--  --%>  :  jsp코드 전체 주석
5. <%@  %>  :  지시어(page지시어, include지시어, taglib선언)(문서의 첫줄에 작성)

* 단점 : ~.jsp문서에 스크립팅요소가 많아지면 소스가 복잡, 가독성 낮아짐.
  * 단점을 보안하기 위해서 JSTL + EL로 변환한다.

<hr>

##### jsp문서에서 한글을 작성하기 위해서 문서의 첫줄에 작성해야하는 것은?

- <%@page contentType="text/html:charset=UTF-8" %>  => WAS가 해석할때 인코딩

- <meta charset="UTF-8"> => 브라우저 해석할 때 인코딩

  두개를 맞쳐서 인코딩을 해줘야한다.



##### java계열의 웹프로그래밍 변천사

- Applet : 완벽한 java소스(JFrame 동일)

  - 자바의 GUI와 Event로 화면구성을 하고 자바소스를 브라우저에서 싱행하기 위해서

    별도의 ~.html문서 작성 <applet class=""/> 이용하여 브라우저에서 동작

    : 자바를 잘하지 못하면 개발이 어렵다.(디자이너와 협업이 안됨)

- Servlet : ~.java소스안에  HTML, CSS, JS를 작성한다.

  - 자바의 기본 문법을 모르면 작성하기 어려움

    디자이너와 협업이 어렵다. 

    코딩이 자바중심에 front언어가 부분적으로 있다.

  - Applet보다 낫지만 java를 알아야만 할수 있다.

- JSP : ~.jsp문서 안에 HTML, CSS, JS를 그대로 작성하고 부분적으로 java코드를 작성한다.

  - 코딩이 중심이 front언어이고, 부분적으로 자바코드로 작성한다.

<hr>

## 지시자

### 1. page지시자



### 2. include 지시자

- 현재 파일에 포함시킬 파일을 넣어서 보여줄수 있다.

```jsp
<%@ include file="파일이름.확장자"%>
```

- 현재 파일을 여러 파일과 합쳐 놓은 것이기 때문에 **하나의 소스로 만들어 컴파일** 해준다.

  ==> 다른 파일에 변수 선언하고 다른 파일에서 변수를 사용할 수 있다.(변수 공유)

  ex) index.jsp에 top.jsp와 footer.jsp를 보여주고 싶다면 

```jsp
<%@ include file="top.jsp" %>
<hr color="red">
<h1>include 지시자</h1>

<hr color="red">

<%@ include file="footer.jsp" %>
```

<hr>

## 액션태그

### include 액션 태그

```jsp
<jsp:include page="  "/>
```

- 현재 파일에 여러 파일을 합쳐져서 보여준다.(include지시자와 같은 결과가 나온다.)

- 컴파일 될때 지시자와는 달리 합친 파일이 **따로 따로 소스가 나누어져 있다.**

- 변수를 공유 하려면 param으로 전달해야한다.

  ```jsp
  <%  
    //이 경우에는 현재 파일에서 값을 받아 처리 하기 때문에 인코딩을 현재파일에 해야함
  	//parameter로 전송되는 데이터 한글 인코딩 처리
  	request.setCharacterEncoding("UTF-8");
  	String addr="서울";
  %>
  <jsp:include page="top.jsp"/>
  <hr color="red">
  
  <h1>action tag include</h1>
  
  <hr color="red">
  <jsp:include page="footer.jsp">
  	<jsp:param value="<%=addr%>" name="addr"/>
  	<jsp:param value="hannah" name="id"/>
  </jsp:include>
  ```

- param으로 footer.jsp에 넘겼으면 footer.jsp에서 받아야한다.

  ```jsp
  <%
  	//parameter로 전송되는 데이터 한글 인코딩 처리
  	//request.setCharacterEncoding("UTF-8");
  
  	//parameter로 전송된 데이터를 받기
  	String id = request.getParameter("id");
  	String addr = request.getParameter("addr");
  %>
  <h2>footer.jsp문서 입니다.</h2>
  <h3><%=addr %></h3>
  아이디 : <%= id %>
  
  <!-- 
  param으로 전송된 데이터 인코딩 처리 
    1)get방식
  	- server.xml문서에 URIEncoding="UTF-8" 설정 필수
  	  (tomcat 8.0부터 자동 설정)
  
    2)post방식
  	- request.setCharacterEncoding("UTF-8") 설정 필수
  
  
  -->
  
  ```

<hr>

- #### 이동방식

  1. WAS이동방식

     - forward방식

       : request와 response를 유지하면서 이동

       방법 :

       ```jsp
       액션 태그 :  <jsp:forward page=" "/>
       
       메소드 :  request.getRequestDispatcher(" url주소").forward(request, response) 
       ```

     - redirect방식

       : request와 response를 새롭게 생성해서 이동

       방법 : 

       ```jsp
       response.sendRedirect(String url);
       ```

  2. webServer - 브라우저 이동방식

     - <a href=""></a> - html문서

     - location.href=" " : script에서 이동

       방법 : 

       ```jsp
       <form action = " ">으로 이동
       ```


<hr>

### forward 액션 태그

- 현재 page에 지정한 page를 덮어 씌어준다.(뒤로 가기 없음)

  ```jsp
  <jsp:forward page="">
      <jsp:param name="" value=""/>
  </jsp:forward>
  <!-- 값을 넘겨 주지 않아도 된다. response와 request가 되기 때문-->
  ```

  - **<jsp:forward page='<%= 변수 + ".jsp"%>' />**
    - forward 액션 태그의 page 속성은 이동할 페이지명을 기술하고 상대경로, 절대경로로 지정할 수 있다.
  - 페이지가 이동할 때  기존 request와 response를 그대로 유지하면서 이동
    - url주소를 보면 전페이지 url주소가 보임
  - forward 액션 태그에서 포워딩되는 page에 parameter 값을 전달할 수 있다.



## JSP내장 객체

#### * 확장자 jsp에서만 쓸수 있는 9개의 내장 객체 reference변수 제공

> ~.jsp문서를 만들어서 서버에게 요청을 하면 ~.java의 servlet문서가 만들어진다.
>
> 이안에 메소드 _jspService(request, response){
>
> 			  	session, application, out,...(내장객체) 선언
>		
> 			   }

- #### request => HttpServletRequest의 refernece

  - ##### 클라이언트의 요청 정보를 받아서 처리하는 주요 메소드를 제공(서버축에서 사용할 때)

  - String value = request.getParameter(String name) ;

    - request로 넘어오는 name에 해당하는 value값 받기

  - request.setCharacterencoding("euc-kr");

    - request로 넘어오는 한글 인코딩 변환

  - String str[] = request.getParameterValues(String name);

    - name에 해당하는 value 여러개 일 때 사용함

  - Enumeration<String> e = request.getParameterNames();

    - request로 넘어오는 name에 대한 정보 가져오기

  - String ip = request.getRemoteAddr();

    - 접속한 클라이언트 ip가져오기

  - Cookie co [] = request.getCookies();

    - 접속한 클라이언트에 저장된 쿠키정보(클라이언트정보)가져오기



- response =>HttppServletResponse의 reference

  - ##### 요청된 결과를 클라이언트쪽으로 보낼때(응답) 필요한 주요 메소드 제공

  서버에서 이동하는 방식
  	1) redirect 방식 : 페이지 이동할 때 기본 request와 response를 버리고 

  				     새롭게 request와 response를 생성한 이동방식
  		response.sendRedirect("url주소" userName="+URLEncoder.encode(변수, "UTF-8"));	
		
  	2)forward 방식 : request와 response를 유지하면서 이동 방식
  		request.getRequestDispatcher("LoginOk.jsp").forward(request, response);	



- #### out

  - 페이지내용을 담고 있는 출력 스트림 객체

    ```out.println();```



- #### session =>javax.servlet.http.HttpSession

  > 브라우저를 start(브라우저를 열었다.) -> stop(브라우저 창을 닫았다.) 할때 까지 유지되는 동안 사용자의 정보를 서버측에 저장하여 유지해주는 것(브라우저당 session생성)
  >
  > ->서버는 무조건 접속이되면 sessionId를 생성하여 각 클라이언트쪽의 쿠키에 저장해놓고 다시 요청되면 그 저장된 쿠크값을 읽어와서 사용자를 구분한다.
  >
  > 유효시간 30분(1800초) 기본 세팅
  >
  > 로그인 -> 로그아웃 기능에 이용한다.

  - String id = session.getId();
    - 세션이 생성되면 자동으로 만들어지는 세션
  - session.setMaxInactiveInterval(시간);
    - 세션 유효시간 설정
  - session.setAttribute(String name ,Object obj);
    - 세션의 정보를 저장
  - session.getAttribute(String name)
    - 세션의 정보를 가져와서 사용
  - session.inValidate()
    - 모든 세션의 정보 지우기



- #### application=> ServletContext

  > 특정한 정보를 서버가 시작해서 종료될때까지 유지 되도록함
  >
  > 서버에 대한 정보를 추출과 웹 어플리케이션단위로 상태정보저장
  >
  > 서버가 start될 때 단 하나의 application이 생성됨
  >
  > stop될때까지 생성된 객체를 계속 사용가능
  >
  > ** application쪽에 정보를 저장하면 모든 user들이 공통으로 사용하는 영역이되고 평생 유지된다.

  - application.setAttribute(String nae, Object value);
    - 정보를 저장하는 기능
  - Object value = application.getAttribute(String name);
    - name에 해당하는 정보를 가져오는 기능
  - application.removeAttribute(String name);
    - name에 해당하는 정보를 삭제하는 기능
  - application.getRealPath(java.lang.String path);
    - 실행되는 문서의 경로를 가져오는 기능
  - application.contextPath();
    - url주소에 사이트를 실행할 수 있는 식별자
  - Enumeration e = application.getAttributeNames();
    - 저장된 정보의 name 가져오는 기능



- #### exception=>java.lang.Throwable의 reference

  > jsp페이지 서블릿 실행시 처리하지 못한 예외 처리

  1. ~.jsp문서 첫줄에 errorPage="" 설정하는 방법

     - 모든 예외를 한페이지에서 처리할때 편리함
     - 예외마다 하는일을 다르게 처리하기에는 불편

  2. web.xml(배포서술자=DD(Deployment Descriptor)) 문서에 예외별 페이지를 설정하는 방법

     - 예외마다 해야할일이 다를 때

     - 예외코드 or 예외 종류별로 페이지를 만들어서 처리할 때 편리함

       ```jsp
       - web.xml문서에 아래에 에러페이지 설정한다.
       <error-page>
           <exception-type>예외 종류</exception-type>
           <location>예외가 발생했을때 이동할 페이지</location>
       </error-page>
       ```


<hr>

## Cookie

- #### cookie=> javax.servlet.http.Cookie

  > 클라이언트의 정보를 클라이언트 pc에 저장함
  >
  > 사용자 측에 대한 정보를 보관해 두었다가 웹서버의 요청에 의해 정보를 원하는 순간에 사용할 수 있다.
  >
  > 한번에 4KB로 용량이 제한되고 300개 까지 저장가능함
  >
  > 작은정보의 형태로 저장되고 오래되면 자동삭제됨
  >
  > 삭제위험, 보안약함 --> 사용자를 분석하거나 사용자의 패턴, 사용자중심의 서비스를 제공할때 많이 사용

- response.addCookie(Cookie co)

  - 클라이언트쪽에 클라이언트의 정보를 저장함

- String getName() : 쿠키 이름 가져오기

- String getValue() : 쿠키 값 가져오기

- Cookie 관련 메소드정리

  - int getMaxAge() => 쿠키의 사용할수 있는 기간에 대한 정보

  - setMaxAge(int max) =>쿠키가 저장되는 기간 설정

      ex) max=0 ->쿠키삭제

    	max=-1 -> 쿠키폴더에 파일이 만들어지지 않지만 브라우저가 종료될때까지 쿠키의 정보는 

    			   저장된 상태이고 브라우저를 닫으면 쿠키정보 사라짐(생략하면 -1이기본)

- Cookie생성자

  - Cookie(String name, String value);

    ex) Cookie cookie = new Cookie("id","hannah")


<hr>

## 에러 상태 코드

1. 500 :  소스상의 코드 에러
2. 404 :  FileNotFoundException :경로 오류
3. 405 :  get방식과 post방식을 구분 못했을 때 요청 방식 오류...
4. 403 :  인증은 되었으나 권한 부족
5. 200 :  성공!
6. 400 :  요청의 형식이 잘못 되었을 때

<hr>

## 한글인코딩 처리 메소드

- ##### parameter로 넘어오는 데이터 처리

1. get방식 : server.xml문서에 URIEncoding="UTF-8" 필요

   		tomcat8.0부터 개선

2. post방식 

   - 소스에 request.setCharacterEncoding(String enc) :설정

<hr>

## scope-서버쪽에 저장

- 웹의 취약점
  - 상태정보를 지속적으로 유지할수 없다.
  - why? 사용자의 요청이 들어오면 request, response완료되면 모든 정보와 상태는 끊긴다.
  - 이런 부분을 해결하기위해 다양한 저장방법을 제공
  - 페이지를 이동할 때 상태정보를 유지시킬것인가에 대한 저장방법이 scope의 개념으로 해결가능하다.

- pageContext -> request -> session -> application (cookie는 포함X-클라이언트에 저장되기 때문)
  - 공통의 메소드(저장, 꺼내기)
    - ~.setAttribute(String name, Object obj);
    - Object obj = ~.getAttribute(String name);
    - ~.removeAttribute(String name);



<hr>
## Servlet문서 작성하기

- 등록할 때 <load-on-startup>설정하면 tomcat이 start될때 생성됨
- <load-on-start>가 없으면 최초의 사용자 요청이 들어올때 생성된다.

- #### 반드시 javax.servlet.http.HttpServlet를 상속받는다.(public class)

  ``` java
  public class A extends HttpServlet{
      //필요한 메소드 재정의해서 기능 부여
  }
  ```

- #### HttpServlet에 있는 관련 메소드

  - ##### init() 

    - 서블릿문서가 초기화될 때 (최초에 처음 실행될때 호출됨)

  - ##### init(ServletConfig config) 

    - ServletConfig는 web.xml문서에 설정되어 있는 서블릿에 대한 환경설정정보를 담고 있는 객체이다.
    - 서블릿이 생성될때 최초에 딱한번 호출되며 초기치파라미터나 생성되는 시점에 해야하는 일들 작성

  - ##### service(ServletRequest request, ServletResponse response)

    - init이 실행될 후 호출됨(서블릿문서 새로고침하면 service실행됨)

    - 사용자 요청이 get/post인지를 구분하여 doGet or doPost호출함

      : service를 재정의하면 이 일을 안한다.

  - ##### doGet(HttpServletRequest request, HttpServletResponse response)

    - 사용자 요청 get방식일 경우 실행됨

  - ##### doPost(HttpServletRequest request, HttpServletResponse response)

    - 사용자 요청 post방식일 경우 실행됨

  - ##### destory() 

    - 서블릿문서가 종료될때 호출함




- #### 서블릿문서를 실행하기 위한 준비작업

  1.  public class
  2.  HttpServlet상속
  3.  필요한 메소드 재정의
  4.  servlet을 등록한다.
      *    1.web.xml문서 등록
      *    2.@annotation 등록

<hr>

- #### 서블릿문서 등록 방법

  1. web.xml 문서에 등록

     ``` xml
     <servlet> <!--객체 생성과 같다.  => t = new Test()와 같다.-->  
     	<servlet-name>t</servlet-name>
         <servlet-class>Test</servlet-class>
         <loac-on-startup>1</loac-on-startup><!--tomcat start될 때 객체 생성-->
     </servlet>
     <!--브라우저에서 요청할때 매핑  http://domain:port/contextPath/요청이름-->
     <servlet-mapping>
     	<servlet-name>t</servlet-name>
     	<url-pattern>/t</url-pattern> <!-- "/"를 꼭 써줘야한다. "/"=conntextPath--->
     </servlet-mapping>
     ```

  2. @annotation 등록



<hr>

- ##### 서블릿문서에서 HttpSession 객체 얻어오는 방법

  ```java
  HttpSession session = request.getSession();
  ```

- ##### 서블릿문서에서 ServletContext객체 얻어오는 방법

  ```java
  ServletContext application = request.getServletContext();
  ```

- ##### 서블릿문서 작성할 때 브라우저에 출력하기 위해 필요한 코드

  ```java
  PrintWriter out = response.getWriter();
  ```

- ##### 브라우저에 한글 출력하기위해 문서 첫줄에 필요한 코드

  ```java
  response.setContentType("text/html:charset=UTF-8");
  ```

- ##### request으로 전달되는 parameter의 post한글 인코딩 처리

  ```java
  requset.setCharacterEncoding("UTF-8");
  ```

<hr>

- #### init-param

  - 서블릿 생성될때 전달되는 초기치 파라미터로 그 서블릿에서만 사용할 수 있는 파라미터 web.xml문서에 선언하는 방법

    ```xml
    <servlet> 
    	<servlet-name>t</servlet-name>
        <servlet-class>Test</servlet-class>
        <init-param>
        	<param-name>addr</param-name>
            <param-value>seoul</param-value>
        </init-param>
        <loac-on-startup>1</loac-on-startup>
    </servlet>
    ```

  - 서블릿문서에서 초기치 파라미터 사용방법

    ```java
    public void init(){
        String addr = super.getInitParameter("addr");
    }
    /////////////////////////////////////////////////////////
    public void init(ServletConfig config){
        String addr = config.getInitParameter("addr");
    }
    ```

<hr>

- #### context-param

  - 모든 서블릿이 공유하기 위한 값을 web.xml문서에 등록하는 방법

    ```xml
    <context-param>
    	<param-name>message</param-name>
        <param-value>servlet</param-value>
    </context-param>
    <!-- 모든 서블릿, 모든 jsp에서 tomcat이 stop할 때까지 언제든지 사용가능-->
    ```

  - init을 서블릿문서에서 사용하는 방법

    ```java
    public class Test extends HttpServlet{
        public void init(){
            ServletContext application = super.getServletContext();
            String message = application.getInitParameter("message");
        }
        public init(ServletConfig config){
            ServletContext application = super.getServletContext();
            String message = application.getInitParameter("message");
        }
    }
    ```

  - init을 jsp문서에서 사용하는 방법

    ```jsp
    String message = application.getInitParameter("message");
    ```



<hr>
## Listener

- #### 정의

  - 등록해 놓으면 tomcat이 start될때 자동으로 생성된다. -> 각 구현객체의 init이 호출된다.
  - 이벤트 처리
  - 어떤 이벤트가 발생했을 때 자동으로 호출되어지는 메소드를 이미로 정의해놓은 Handler이다.

- #### Listener 작성 방법

  1. XxxListener를 구현하는 구현 객체를 만든다.

     ```java
     public class AppListener implements Xxx{
          //메소드 재정의
     }
     ```

  2. 메소드 재정의 한다.

  3. Listener등록한다.(둘중에 하나만 써야한다.)

     - web.xml문서

       ```xml
       <listener>
       	<listener-class>listener클래스 이름 입력</listener-class>
       </listener>
       ```

     - @Annotation등록

       - 구현클래스 위에 @WebListener

       (web.xml에 <listener></listener>등록하는 거와 같다.) 

- #### Listener의 종류

  1. ServletContextListener(implements해줘야한다.)

     - tomcat(서버)이 start or stop될 때 호출되는 이벤트
     - 주로 프로젝트가 배포될때(open) 사정 초기화 작업 or 전체적인 환경설정을 세팅할 때 주로 사용

     1-1. ServletContextAttributeListener : 속성이 변경될때 호출

  2. HttpSessionListener

     - session이 생성될때 : 브라우저 start 될때 호출되는 이벤트
     - session이 종료될때 : session.invalidate(), session timeout되었을 때 호출되는 이벤트
     - 브라우저의 x를 클릭했을 때에는 이벤트 발생 안됨

  3. ServletRequestListener

     - 사용자 요청이 될때, 요청이 완료될때 호출되는 이벤트



<hr>

## Excutor

- 병렬처리 프로세스를 분산시켜 좀더 빠르게 작업을 수행 할수 있도록 하는 것

  * JDK1.5에서 만들어짐. 병렬처리가 가능한 thread프레임워크를 제공함

    1. Executor : 기본 thread(thread실행에 관련된 메소드만 제공)

    2. ExecutorService : Executor인터페이스를 확장하여 thread라이프사이클 관리까지 해주는 주요 메소드 제공한다.

       (thread실행 + 안전하게 종료할 수 있도록 다양한 메소드 제공한다.)



## Filter

- #### 정의

  - 등록해 놓으면 tomcat이 start될때 자동으로 생성된다. -> 각 구현객체의 init이 호출된다.

  - 사용자 요청이 있을 때 중간에 filter가 그 요청을 가로채서 **사전처리**하고, 실제 타겟대상을 호출해준후 다시 filter로 돌아와 **사후처리**하고 응답해주는 것.

  - 주로 application영역에서 공통으로 사용해야하는 작업을 필터에 만들어놓고 처리한다.

    (유지보수, 재사용성이 좋아짐) 

    ex) post방식 Encoding, log기록, transaction처리, session유무체크, 예외처리, 

          사용자가 보내오는 parameter정보 필터링 하기

- #### Filter 작성방법

  1. XxxFilter를 구현하는 구현 객체를 만든다.

     ```java
     public class className implements Filter {
     
     }
     ```

  2. 메소드 재정의한다.

     ```java
     public void init(FilterConfig fConfig){
         //init-param으로 전달되는 값 받기
         String value = fConfig.getInitParameter("id");
     }
     public void doFilter (ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
      	//사전처리
         
         chain.doFilter(request, response); //실제 타겟대상 호출
         //사후 처리
     }
     ```

  3. 등록 방법

     1. web.xml문서에 작성

        ```xml
        <filter>
        	<filter-name></filter-name>
            <filter-class></filter-class>
            <init-param>
            	<param-name></param-name>
                <param-value></param-value>
            </init-param>
        </filter>
        <filter-mapping>
        	<filter-name></filter-name>
        	<url-pattern></url-pattern>  <!-- ex) /* | *.jsp |/폴더/*.jsp -->
            <servlet-name></servlet-name>
            
        </filter-mapping>
        ```

     2. @annotation등록

        - 구현 클래스 위에 @WebFilter("/urlpattern")
        - 구현 클래스 위헤 @WebFilter({urlpattern = {}, initParam = {} })
          - initParam이 있을때 써준다.

## EL(Expression Language)

- 표현 언어 내장객체(생략 가능-이름중복확인하고 생략)

  - pageScope
    - page기본객체에 저장된 속성
  - requestScope
    - request 기본객체에 저장된 속성
  - sessionScope
    - session기본객체에 저장된 속성
  - applicationScope
    - application기본객체에 저장된 속성

  ```jsp
  //3개다 같은 뜻!
  <%= session.getAttribute("id")%>님
  ${sessionScope.id}님
  ${id}님
  
  요청 parameter의 name에 해당하는 값 가져옴
  ${param.name} = request.getParameter("name");
  ```



- 사용방법

  ```jsp
  <h1>EL - 표현 언어</h1>
  <%-- \를 붙이면 문자취급해준다. --%>
  \${5} = ${5} <br>
  \${5+3} = ${5+3} <br>
  \${5/2} = ${5/2} <br>
  \${5 gt 3} = ${5 gt 3} <br>
  \${10 lt 3 and 6<3} = ${10 lt 3 and 6<3} <br>
  
  ```


## JSTL

- jsp에서 표준으로 자주사용하는 부분을 미리 태그로 만들어 놓은것
- 종류 : core, XML, 국제화 , DB, 함수



- ### 자주사용하는 코어 JSTL 태그

    <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%> : 맨위에 써줘야함

    1. ##### c:out

         ```jsp
         <c:out value="값 | 변수명" escapeXml="true|false" />
         escapeXml="true" 는 값에 태그 있으면 문자로 출력됨.
         ```

    2. ##### c:set

         ```jsp
         <c:set var="이름" value="값" />
         주의 : value의 값은 무조건 String
                만약 value="${20}" 이면 숫자 20
                     value="${'20'}" 이면 문자 20 
                     value="20"  이면 문자 20 
         ```

    3. ##### c:remove 

         ```jsp
         이름에 해당하는 값 지우기
         <c:remove var="이름" />
         ```

    4. ##### c:catch

         ```jsp
         <c:catch var="이름">
            예외발생 가능성 코드
         </c:catch>
         ```

    5. ##### c:if

         ```jsp
         <c:if test="조건식" var="결과저장할이름" >
         	결과가 true일때 실행문장.
         </c:if>  
         ```

    6. ##### c:choose

         ```jsp
         <c:choose>
             <c:when test="조건식"> 실행문장 </c:when>
         	<c:when test="조건식"> 실행문장 </c:when>
         	<c:when test="조건식"> 실행문장 </c:when>
         	....
         	<c:otherwise> 위조건이외의 경우 실행문장 </c:otherwise>
         </c:choose>
         ```

    7. ##### c:forEach

         ```jsp
         <c:forEach var="이름" begin="시작" end="끝" step="단계"
            items="항목" varStatus="현재상태에대한값" >
         
            ${상태나타내는변수.index}
            ${상태나타내는변수.count}
            ${이름}
         </c:forEach>
         ```



  <%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>

  - fmt:formatNumber

    ```jsp
    <fmt:formatNumber value="숫자"/>
    숫자를 3자리마다 ,를 찍어서 보여준다.
    ```




