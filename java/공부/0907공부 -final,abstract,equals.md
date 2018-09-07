# 공부(0907) -final,abstract,equals

### final(상속불가, 생성가능)

1. variable

   - 변수 앞에 final이 오면 상수가 된다.(변화하지 않는 값)
     - 값 변경 불가, 상수는 모두 대문자로 표현
     - **반드시 초기화해야한다.(전역변수도 초기화해야함)**

2. Method

   - method 앞에 오면 overriding(재정의) 불가

     ```public final void aa(){  }```

3. class

   - **class앞에 오면 상속 안됨**(객체 생성은 가능)

     ​	```final class Test{}```

<hr>

### abstract(상속가능, 생성불가)

1. variable

   - 변수 앞에 올 수 없다.

2. Method

   - method 앞에 abstract 붙으면 선언부만 있고 구현부 없다.(기능 X)

     ```public abstract void aa();``` ;으로 끝남

     	서브 class에서 재정의 하기 위해 존재

   - **abstract method를 가지고 있는 class는 반드시 abstract class로 선언해야한다.**

3. class

   - abstract class는 **생성할 수 없다**.(new 사용안됨)

   - 다른 class의 부모(Super)가 되기 위해 존재

   - 상속관계에 있을 때 superclass가 abstract method를 가지고 있으면  서브 class에서 abstract method 재정의 해야한다.

     - 만약, 재정의 하지 않으면 서브 class는 abstract으로 선언되어야 하며 객체생성 할 수 없다.

       ```abstract class  A{  }```

<hr>

### package

- 문서 맨 첫줄에 한번만 쓸 수 있다.

<hr>

### import

- 문서안에 첫 번째 줄에 작성하여 **여러개 선언가능**

- java.lang은 자동으로 import된다.

<hr>

### equals(Object obj)메소드 

##### 리턴 boolean

- 두 객체의 주소를 비교하여 맞으면 true, 틀리면 false을 리턴해준다.

```java
class Test{
    
}
Test t1 = new Test();
Test t2 = new Test();
Test t3 = t1;

if(t1 == t2) //주소값 비교
if(t1.equals(t2))	//주소값 비교
    
//////////////////////////////////////////
    
String s="안녕";
String s2 = "안녕";
String s3 = new String("안녕");

if(s1==s2)  //주소값을 비교하는 것
if(s1.equals(s2))  //문자열 비교(String은 부모에 있는 Object를 재정의 한 것)
** String은 equals메소드를 재정의 했고 그 기능은 문자열 비교한다.
```

##### String은 값을 변경할 수 없다. 

##### 우리가 변경했던것은 기존의 String을 가비지콜렉터로 만들고 새로운 객체를 만든다.