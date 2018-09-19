# 0918공부 -IOstream

### IOstream(Input/Output)

```java
import java.io.*;
```

- 예외 처리를 꼭 해줘야한다.(try/catch/finally)  -- 코드가 길어진다.

- 반드시 close로 반납을 해줘야한다.

  - 예외처리로 넘겨줘야함

  ```java
  try{
      
  }catch(IOException e){
     
  }finally{
      try{
      	fis.close();
      }catch(IOException e){
          
      }
  }
  ```

- 단방향 stream

  - 읽고 쓰기를 동시에 못함
  - 읽기와 쓰기 클래스가 따로있다.

**InputStream, OutputStream, Reader, Writer는 abstract이기에 <- 상속 subclass 존재 **

abstract- 상속 가능, 생성 불가능(subClass를 사용해야함)

-- 메소드 이름은 같아도 기능이 다르다.(read, write)

- byte단위(int)
  - 하나의 byte씩만 읽는다. (한국어는 하나의 byte=2byte로 인식한다.)
  - char로 변환, String으로 변환(new String(   ))
  - String을 byte로 변환(getBytes())
  - Inputstream : 읽기  -> ~.read()  =>FileInputStream(subClass)사용
  - Outputstrean : 쓰기  -> ~.write()   =>=>FileOutputStream(subClass)사용
    1. 생성 = 연다
    2. 읽기 or 쓰기
    3. 닫기
- 문자 단위(한글 쓰기에 용이함 -String)
  - byte와 상관없이 한글자씩 읽는다.(한글깨짐 없음)
  - Reader : 읽기   -> ~.read()  =>FileReaderStream
  - Writer : 쓰기   -> ~.write()  =>FileWriterStream



- File객체(생성(기본 생성자는 없음), 상속 가능)
  - 어떤 방식으로 쓸것인지
  - 파일의 내용을 읽어 오는 것, 폴더 생성, 파일 생성, 내용 입력 ...

--용어 정리

- NodeStream
  - 입/출력 장치에 직접 연결되는 스트림
  - **반드시 필요**

- FilterStream(보조 스트림)
  - **옵션**(필요에 따라 사용가능)
  - 0개 이상 사용가능
  - 생성자에 인수를 NodeStream으로 사용한다.
  - Buffered클래스를 많이 쓴다.
    - 속도차이가 많이 난다.
    - readLine() : 한줄 씩 읽기
    - newLine() : 개행해주기
  - InputStreamReader : InputStream을 Reader로 바꾸는 클래스



### 변경된 문법

```java
//원래의 문법
try{
    
}catch(IOException e){
    
}finally{
    try{
        fis.close();
    }catch(IOException e){
        
    }
}
```

```java
//바뀐 문법
try(FileInputStream fis = new  ....()){
    //close를 try()안에 써줌으로써 finally와 finally안에 try/catch문을 안쓴다.
    //코드가 굉장히 짧아짐
    //아직 실무에서는 많이 사용하진 않는다.
}catch(IOException e){
    
}
```



#### 데이터영속성

1. 자료구조
2. 파일 IO
3. JDBC

### 객체를 직렬화 - 파일에 저장

1) 반드시 Serializable 구현한다.

2) 생성자, 메소드 직렬화 안됨.

3) 필드만 직렬화 (static, transient키워드는 직렬화대상에서 제외됨)

4) 객체를 저장하려면 보조스트림이 필요하다(ObjectOutputStream)