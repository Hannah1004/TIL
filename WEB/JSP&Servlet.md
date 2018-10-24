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

  ==> 다른 파일에 변수 선언하고 다른 파일에서 변수를 사용할 수 있다.

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

- 변수를 공유 하려면 param을 써야한다.

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

       ​	액션 태그 :  <jsp:forward page=" "/>

       ​	메소드 :  request.getRequestDispatcher(" url주소").forward(request, response) 



     - redirect방식

       : request와 response를 새롭게 생성해서 이동

  2. webServer - 브라우저 이동방식

     <a href=""></a> - html문서

     location.href=" " : script에서 이동

     ```html
     <form action = " ">으로 이동
     ```

<hr>

### forward 액션 태그

- 현재 page에 지정한 page를 덮어 씌어준다.(뒤로 가기 없음)

  ```jsp
  <jsp:forward page=""/>
  <!-- 값을 넘겨 주지 않아도 된다. response와 request가 되기 때문-->
  ```

  - **<jsp:forward page='<%= 변수 + ".jsp"%>' />**
    - forward 액션 태그의 page 속성은 이동할 페이지명을 기술하고 상대경로, 절대경로로 지정할 수 있다.
  -   forward 액션 태그에서 포워딩되는 page에 parameter 값을 전달할 수 있다.



## JSP내장 객체

#### * 확장자 jsp에서만 쓸수 있는 내장 객체

- request => HttpServletRequest의 refernece

  - ##### 클라이언트의 요청 정보를 서버축에서 사용할 때

  - String value = request.getParameter(String name) ;

    - request로 넘어오는 name에 해당하는 value값 받기

  - request.setCharacterencoding("euc-kr");

    - request로 넘어오는 한글 인코딩 변환

  - String str[] = request.getParameterValues("hobby");

    - name에 해당하는 value 여러개 일 때 사용함

  - Enumeration<String> e = request.getParameterNames();

    - request로 넘어오는 name에 대한 정보 가져오기

  - String ip = request.getRemoteAddr();

    - 접속한 클라이언트 ip가져오기

  - Cookie co [] = request.getCookies();

    - 접속한 클라이언트에 저장된 쿠키정보(클라이언트정보)가져오기

- response

  서버에서 이동하는 방식
  	1) redirect 방식 : request, response를 새롭게 생성해서 이동방식
  		response.sendRedirect("LoginOk.jsp userName="+URLEncoder.encode(userName, "UTF-8"));	

  	2)forward 방식 : request와 response를 유지하면서 이동 방식
  		request.getRequestDispatcher("LoginOk.jsp").forward(request, response);	

  ​	

- out

- session

  - String id = session.getId();
    - 세션이 생성되면 자동으로 만들어지는 세션
  - session.setMaxInactiveInterval(시간);
    - 세션 유효시간 설정
  - session.setAttribute(" " ," ");
    - 세션의 정보를 저장

- application

- exception

<hr>

## 에러 상태 코드

1. 500 :  소스상의 코드 에러
2. 404 :  FileNotFoundException :경로 오류
3. 405 :  get방식과 post방식을 구분 못했을 때 요청 방식 오류...
4. 403 :  인증은 되었으나 권한 부족
5. 200 :  성공!
6. 400 :  요청의 형식이 잘못 되었을 때















