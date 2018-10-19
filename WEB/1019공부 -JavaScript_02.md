# 1019공부 -JavaScript2(추가)

## 서버

- HTML, CSS, JavaScript
  - 브라우져에서 실행 -모든 소스들의 클라이언트쪽으로 다운로드되어 실행



- DB + JSP(전송된 데이터를 받아 처리해주는 언어)

  form -> 전송을 하면서 값을 들고 감


- ### img관련 JavaScript

  - 자바스크립트내에서 img객체에 접근하는 방법

    1. document.images[번지수].속성 //이미지가 순서대로 배열로 들어간다.
    2. document.img이름.속성
    3. img에 id를 설정하고 id로 찾기(document.getElementById("아이디"))

    ```javascript
    function imgInfo(index) {
      		var str="";
    		switch(index){
    		case 1: //고양이
    			str +="name : " + document.images[0].name+"<br>";
    			str +="width : " + document.images[0].width+"<br>";
    			str +="height : " + document.images[0].height+"<br>";
    			str +="src : " + document.images[0].src+"<br>";
    			str +="border : " + document.images[0].border+"<br>";
    			str +="alt : " + document.images[0].alt+"<br>";
    			break;
            }
      		document.getElementById("result").innerHTML=str;
    	}
      	
      	function imgInfo2(imgName){
      		var str="";
      		var img=eval("document."+imgName);
      		str +="name : " + img.name+"<br>";
    		str +="width : " + img.width+"<br>";
    		str +="height : " + img.height+"<br>";
    		str +="src : " + img.src+"<br>";
    		str +="border : " + img.border+"<br>";
    		str +="alt : " + img.alt+"<br>";
    		
    		document.getElementById("result").innerHTML=str;
      	}
      	
    ```
