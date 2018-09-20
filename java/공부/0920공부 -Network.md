# 0920공부 -Network

=>```import java.net.*;```

### Network 방법

1. ##### tcp방식(ex)email) -많이 사용

   - ServerSocket, Socket(으로 server와 client를 연결)

   - 연결성 통신방법, Network 부담 높음
   - 실시간 처리
   - 데이터 손실 위험이 적음

2. ##### UDP방식(ex)우체국)

   - DatagramSocket, DatagramPacket

   - 비연결성 통신방법, Network 부담 낮음

   - 필요할 때만 연결해서 사용
   - 데이터 손실 가능성 높음



<hr>

### 용어 정리

1. InetAddress :접속한 client의 IP와 port번호 알아오는 주소
2. URL/URI
3. port : 하나의 IP에 여러 응용프로그램을 분리해주는 번호(중복되면 X)

 

<hr>

### Server &  Client 연결

#### server 생성

```java
import java.net.*;

ServerSocket server = new ServerSocket(int port);

while(true){ //client가 들어올 때마다 돌아간다.
    Socket sk = server.accept();  //client접속 대기중

    //byte단위로 읽기(client가 보내온 데이터)
    InputStream is = sk.getInputStream(); 
    //byte단위로 출력(client에게 데이터를 보내줌)
    OutputStream os = sk.getOutputSteam();

	~.close();  //접속이 끊김
}
```

#### client(->server에 연결)

```java
Socket sk = new Socket(int port);//server port와 같아야함 //prot번호로 접속

//byte단위로 읽기(server가 보내온 데이터)
InputStream is = sk.getInputStream(); 
//byte단위로 출력(server에게 데이터를 보내줌)
OutputStream os = sk.getOutputSteam();

~.close();  //접속이 끊김
```















