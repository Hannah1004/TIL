# JSP&Servlet  -파일 업&다운로드

## 파일 업로드

1. ##### 파일 업로드에 필요한 라이브러리 다운로드

   (http://www.servlets.com/cos/)

2. ##### 다운로드한 라이브러리를 압축을 풀어 lib폴더에 있는 cos.jar파일을 WEB-INF/lib에 넣는다.

- 파일 업로드 다운로드 폼

  - method는 반드시 **post방식**
  - **enctype="multipart/form-data"**필수
    - request로 데이터를 받을 수 없음
    - 

  ```jsp
  <form name="f" action="upLoadPro.jsp" method="post" 
   enctype="multipart/form-data">
     이름 : <input type="text"  name="name"><br>
     제목 : <input type="text"  name="subject"><br>
     파일첨부 : <input type="file"  name="file"><br>
      <input type="submit"  value="전송">
      <input type="reset"  value="취소">
  </form>
  ```








