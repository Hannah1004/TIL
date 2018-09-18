# 0918공부 -IOstream

### IOstream(Input/Output)

```java
import java.io.*;
```

- 단방향 stream
  - 읽고 쓰기를 동시에 못함
  - 읽기와 쓰기 클래스가 따로있다.
- 반드시 close로 반납을 해줘야한다.
  - 예외처리로 넘겨줘야함

**InputStream, OutputStream, Reader, Writer는 abstract이기에 <- 상속 subclass 존재 **

abstract- 상속 가능, 생성 불가능(subClass를 사용해야함)

-- 메소드 이름은 같아도 기능이 다르다.(read, write)

- byte단위(int)
  - Inputstream : 읽기  -> ~.read()  =>FileInputStream(subClass)
  - Outputstrean : 쓰기  -> ~.write()   =>=>FileOutputStream(subClass)
    1. 생성 = 연다
    2. 읽기 or 쓰기
    3. 닫기
- 문자 단위(한글 쓰기에 용이함 -String)
  - Reader : 읽기   -> ~.read()
  - Writer : 쓰기   -> ~.write()



- File객체(생성(기본 생성자는 없음), 상속 가능)
  - 어떤 방식으로 쓸것인지

--용어 정리

- NodeStream
  - 입/출력 장치에 직접 연결되는 스트림
  - 반드시 필요

- FilterStream
  - 옵션(필요에 따라 사용가능)
  - 0개 이상 사용가능