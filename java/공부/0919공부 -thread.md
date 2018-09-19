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

  	- 메소드의 동기화는 메소드의 지정자인 키워드 synchronized를 기술

  2) 블록의 동기화 

   - 블록의 동기화는 synchronized (Object) {…}Object는 잠금장치를 수행하는 객체

#### thread 간 협업

- 동기화 안에서만 사용할 수 있는 메소드
  - wait()  --스레드를 일시정지 상태로 만들기(대기) --예외 처리 해줘야한다.(try/catch)
  - notify() ,  notifyAll() --wait()에 의해 일시정지상태 였던 thread를 깨우다.



<hr>

### thread  상태 제어

##### 1. 주어진 시간동안 일시정지(sleep)

- sleep은 예외처리를 반드시 해줘야한다.

```java
try{
	Thread.sleep(숫자);  //숫자만큼 스레드를 일시 정지 상태로 만듬
	//ex)1000 => 1초, 100 => 0.01초
}catch(InterruptedException e){ }
```

##### 2. 다른 스레드에게 실행 양보(yield())

- 다른 스레드에게 실행을 양보하고 자신은 실행 대기 상태로 가는 것

##### 3. 다른 스레드의 종료를 기다림(join())

- 다른 스레드가 종료될 때까지 기다렸다가 메인스레드 실행



<hr>

### thread의 안전한 종료

##### 1. stop 플래그를 이용하는 방법

- 스레드는 run()메소드가 끝나면 **자동적으로 종료**
- run()메소드가 정상적으로 종료되도록 유도하기 위해 stop()을 쓴다.

```java
//스레드를 종료시키기 위해 stop필드를 true로 변경
Thread.setStop(true);
```



##### 2. interrupt()메소드를 이용하는 방법

- 스레드가 일시 정지 상태에 있을 때 interruptedException예외를 발생시키는 역할



### 데몬 스레드

- 주 스레드의 작업을 돕는 **보조적인 역할**을 수행하는 스레드
- 주 스레드가 종료되면 데몬 스레드는 **강제적으로 자동 종료**