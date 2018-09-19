# 0919공부 -thread(스레드)

### 멀티 스레드

- **하나의 응용프로그램에서 여러개의 작업을 하는 것**
- 응용프로그램 두개를 동시에 하는 것은 테스킹이다.

#### 1. thread만드는 방법(상속-extends)

```java
class A extends Thread{
    //반드시 재정의 해야하는 메소드
    public void run(){
        //thread로 동작할 기능을 작성;
        
    }
}
public static void main(String [] args){
    A a = new A();
    //a.run();  <-이렇게 하면 안됨
    //thread pool안으로 들어가야한다.
    //start로 호출하면 알아서 호출된다.
    a.start();  //  => Thread준비 상태
}
```

#### 2. thread만드는 방법(구현-implements)

- 기능을 만드려면  반드시 오버라이딩을 해야한다.
- 상속이나 구현밖에 안된다.
- 오버라이딩을 할수 있는 인터페이스(Runnable)를 implements를 해줘야한다.

```java
class B implements Runnable{  //Runnable에 있는 메소드 재정의(하나밖에 없음-run)
    public void run(){
    }
}
public sttic void main(String [] args){
    B b = new B();
    //thread 생성
    //Runnable을 구현해줄수 있는 기능
    Thread t = new Thread(b);
    t.start();
}
```



<hr>

### thread 동기화

- 다중스레드에서 임계영역의 독점적 처리 해결방법

- 동기화 방법

  1) 메소드의 동기화 

  ​	- 메소드의 동기화는 메소드의 지정자인 키워드 synchronized를 기술

  2) 블록의 동기화 

  ​	- 블록의 동기화는 synchronized (Object) {…}Object는 잠금장치를 수행하는 객체

- 동기화 안에서만 사용할 수 있는 메소드

  - wait()  --스레드를 일시정지 상태로 만들기(대기) --예외 처리 해줘야한다.(try/catch)
  - notify() ,  notifyAll() --wait에 의해 일시정지상태 였던 thread를 깨우다.