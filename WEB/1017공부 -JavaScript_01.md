# 1017공부 -JavaScript_01

- #### javascript 주석 : //(한줄 주석), /* */(여러줄 주석)이다.

- ### 이벤트 적용방법 3가지

  1. 태그에 직접 적용

     ```html
     <h1 onmouseover="document.bgColor='pink'"
         onmouseout="document.bgColor='blue'"
         onClick="alert('스크립트 배우는날');alert('오늘은 10월 17일')"
     >오늘은 javaScript배우는날</h1>
     <!-- h1태그에 이벤트 직접 주기 -->
     ```

  2. ##### ```<script></script>```만들어서 적용하기

     ```html
     <!-- script는 body가 만나기전에 실행된다. -->
     <head>
         <script type="text/javascript" language="javascript">
         	alert("난 언제 출력될까?"); //맨처음 출력된다.
             //마우스 over
             function test1(){
                 document.bgColor="pink";
             }
             
             //클릭했을 때
             function test2(){
                 alert("스크립트 배우는날");
                 alert("오늘은 10월 17일");
             }
         </script>
     </head>
     <body>
         <!--
     		위에서 만든 함수를 불러서 호출해줘야한다.
     	-->
         <h1 onmouseover="test1()" onClick="test2()">
             오늘은 JavaScript배우는 날~
         </h1>
     </body>
     ```

     - HTML 마크업을 할 수 있다.

       ```html
       <body>
           <script>
           	//HTML 마크업을 할 수 있다.
               document.write("안녕하세요<br>");
               document.write("<h2>신기하다~</h2>")
           </script>
       </body>
       ```

  3. ##### 외부에 ~.js파일을 만들어서 적용하기

     - html문서

     ```html
      <head>
       <meta charset="UTF-8">
       <title>JavaScript적용방법</title>
          <!-- 외부의 js를 연결하는 방법 -->
       <script src="basic.js">
       	//src속성이 적용된 script내부의 코드는 모두 무시된다.  
         //꼭 넣어야한다면 밑에 <script>를 열러서 쓰면됨
       </script>
      </head>
      <body>
      <!-- 
     		이벤트 적용방법 3가지
     			1) 태그에 직접 적용하기
     			2)<script></script> 만들어서 적용하기
     			3)외부에 ~.js파일을 만들어서 적용하기
      -->
     
     	<h1 onmouseover="test1()" onmouseout="test2()" 
     	onClick="test3()">오늘은 JavaScript 배우는 날~</h1>
     </body>
     ```

     - javascript문서

     ```javascript
     //마우스 over
     function test1(){
     	document.bgColor="pink";	
     }
     
     //마우스 out
     function test2(){
     	document.bgColor="white";
     }
     
     //클릭했을 때
     function test3(){
     	alert("스크립트 재미있다");
     	alert("오늘은 점검있는 날");
     	alert("좋다 좋아~");
     }
     ```

<hr>

- ### 변수

  - 변수 선언

    - 전역변수는 var를 생략가능하다. 
    - 함수 내에서 처음 선언되는 변수에 var를 생략하면 전역변수가 된다.

    ```javascript
    var a=10;
    addr="서울"; 
    function test1(){
    	var a=5;  //지역변수
        message="안녕하세요";  //전역변수는 다른 함수에서 사용가능하다.
        	document.write("a = " + a +"<br>");  //a=5
    		document.write("this.a = " + this.a + "<br>");  //a=10
    		document.write("name = " + name + "<br>");  //name = 
    		document.write("addr = " + addr + "<br>");  //addr=서울
    		document.write("message = " + message+ "<br>"); //message=안녕하세요
    }
    
    function test2(){
        	document.write("a = " + a +"<br>"); //a=10
    		document.write("this.a = " + this.a + "<br>");  //a=10
    		document.write("name = " + name + "<br>");
    		document.write("addr = " + addr + "<br>");  
    		document.write("message = " + message+ "<br>"); //message=안녕하세요
    }
    //함수 호출
    test1();
    test2();
    ```

<hr>

- ### 함수 

  - ##### 내장함수

    - alert("문자열") :  문자열에 원하는 내용을 입력해주면 대화상자가 나타남
    - prompt("문자열","초기값") : 화면에 대화상자를 표시하고 사용자로부터 원하는 정보를 키보드로 입력 받을 수 있음
    - confirm("문자열") : 문자열에 원하는 내용을 나오면 대화상자가 나타남 , 사용자가 "확인","취소"버튼 중 하나를 선택할 수 있음
    - eval(문자열) : 문자열로 입력된 수식을 계산하는 함수
    - String(객체) :  객체를 문자열로 변환하는 함수



  - ##### 문자열을 숫자로 바꾸기

    - parseFloat(문자열) : ()숫자로 구성된 문자열을 입력받아 실수값을 돌려준다.
    - parseInt(문자열, 진수) : 문자열을 정수형으로 바꾸어주는 함수, 문자열 대신 실수를 넣으면 정수형으로도 바꾸어줌(소수점자리 버림)



  - ##### 외부 함수

    - 매개변수가 없는 함수 - function 함수이름(){}
    - 매개변수가 있는 함수 - function 함수이름(인수(ex.color,a,b)){ return은 필요하면 사용}

<hr>
- ### 객체 = 속성 + 메소드

  - 공통적인 특성을 가진 속성이나 동작들을 묶어놓은 그룹

  - 객체 사용법

    - 마침표(.) 사용

    - 객체명.속성명 or 객체명.메소드명

      ex) document.write("문자열");

    - 상위객체이름.하위객체이름.속성 or 메소드

  - ##### 객체 조작문

    - New()

      - 만들어져 있는 객체 혹은 내장객체를 이용하여 새로운 객체를 만들때 사용

        객체변수 = new 객체명();

    - This

      - 이것은 객체타입에 상관없이 현재의 객체를 지칭하는 키워드

        this.속성 or this.하위객체

    - typeof

      - 변수의 데이터형을 알아내기 위해서 사용

        typeof"문자열"  => "String"

        typeof 숫자 => "number"

<hr>

- ### 내장객체

  - ##### Date : 시스템에 있는 날짜와 시간을 js에서 사용할 수 있게 해줌

    - getXxx <= Xxx에 해당하는 곳을 가져온다.

    - setXxx <= Xxx에 해당하는 곳이 바뀐다.

      ```html
      <!-- 오늘 날짜, 시간 가져오기 -->
      <script>
      	var today = new Date();  //현재날짜와 시간설정
          document.write("today.getFullYear() = " + today.getFullYear() +"<br>");
      	//1월=0, 2월=2 ... 12월=11
      	document.write("today.getMonth() = " + today.getMonth() +"<br>");
      	document.write("today.getDate() = " + today.getDate() +"<br>");
      	
      	//요일 -> 0=일, 1=월, 2=화, ...6=토
          //요일을 배열방에 넣어서 꺼내온다.
      	document.write("today.getDay() = " + today.getDay() +"<br>");
      	var yoil = ["일","월","화","수","목","금","토"];
      	document.write("몇요일인가 = " + yoil[today.getDay()]+"요일" +"<br>");
      
      	document.write("today.getHours() = " + today.getHours() +"<br>");
      	document.write("today.getMinutes() = " + today.getMinutes() +"<br>");
      	document.write("today.getSeconds() = " +today.getSeconds() +"<br>");
      
      	//출력 내용 : 년도. 월. 일. 시간(오전/오후 시:분:초)
      	document.write("today.toLocaleString() = "+today.toLocaleString());
      </script>
      ```

    -  날짜 계산 하기

      > (날짜 - 날짜) => ms단위로 나옴
      >
      > (날짜 - 날짜)/1000  => **초**단위로 나옴
      >
      > (날짜 - 날짜) /1000/60 => **분**단위로 나옴
      >
      > (날짜 - 날짜) /1000/60/60=> **시**단위로 나옴
      >
      > (날짜 - 날짜) /1000/60/60/24=> **일**단위로 나옴  

  - ##### String : 글자모양, 위치이동, 문자열 다루기 등을 할수 있게 메소드 제공

    - new 연산자를 사용하지 않음

      "문자열".메소드()

      "문자열".속성

<hr>

- ### 이벤트

  | Event핸들러 | 설명                                                      |
  | ----------- | :-------------------------------------------------------- |
  | onload      | 문서가 읽혀지는 순간 함수나 명령줄을 실행하고자 할때 발생 |
  | onUnload    | 현재 문서를 떠날때 발생                                   |
  | Onerror     | 문서나 이미지로딩이 에러 발생 할때                        |
  | Onfocus     | 창이나 텍스트박스등을 선택하여 포커스가 주어질 때         |
  | Onblur      | 창이나 텍스트박스를 떠나 포커스가 해제될 때               |
  | Onclick     | 버튼이나 링크등을 마우스로 클릭할때                       |
  | Ondblclick  | 마우스를 더블클릭할 때                                    |
  | Onchange    | 입력양식필드에서 값이 바뀌었을 때                         |
  |             |                                                           |




