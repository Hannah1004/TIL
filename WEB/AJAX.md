# AJAX

- js와 jQuery로 만드는 기술



- jQuery에서 제공하는 ajax관련 함수

  1. $().load()

     - 서버에서 온 응답결과를 화면에 그대로 반영할때 사용

       ```js
       $("").load("서버이름");
       ```

  2. $.getJSON()

  3. $.get()

  4. $.post()

  5. $.ajax({key:value, key:value, ..... })

     ```js
     $.ajax({
     	type : "get",  //전송방식(get, post)사용
     	url : "",   //서버 요청 주소
     	dataType : ,  //서버가 보내주는 데이터 타입(text, html, xml, json)
     	//data : ,   //서버에게 보내는 data(parameter정보)
     	success : function(){},   //요청결과가 성공했을 때 콜백 함수
     	error : function(){}   //요청결과가 실패했을 때 콜백 함수
     });
     ```
