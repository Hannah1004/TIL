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

