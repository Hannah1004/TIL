# 0911공부 -Exception(예외)

### * 필드 종류 

 - 인스턴스 필드 - 생성되어야만 만들어 지는 필드
 - static필드 - 생성없이 만들어지는 필드



### Exception(예외 처리)

- 비체크 예외 = 실행시 발생하는 예외로 예외처리는 선택적으로...(RuntimeException)
- 체크 예외 = 컴파일시 반드시 예외처리 필수!!



### 예외 처리 방법

1. 직접처리 => try{ }  catch( ){ }

   ```java
   try{
       //예외가 발생 가능성이 있는 코드(여러개를 나열할 수 있다.)
       //예외가 발생하면 catch문으로 이동한다.
       //catch or finally가 와야한다.(혼자 쓸 수 없다.)
   }catch(예외종류 참조변수){
       //try에서 발생한 예외가 예외종류 참조변수에 해당한 경우 처리해준다.
       //예외를 처리하는 코드
       //예외가 발생했을 때 실행하는 문장
   	//catch문을 여러개 쓸 때 sub클래스를 먼저 써준다.(Exception은 맨 마지막에)
   }catch(Exception e){
    	//try에서 발생한 예외의 모든 것을 처리해준다.   
   }finally{
       //예외 발생경우 상관없이 무조건 실행
       //여기 있는 코드는 try블록이 끝나면 무조건 실행된다.
       //finally는 생략이 가능하다.
   }
   
   ```

2. 던지기 => throws (임시 방편, 결국엔 직접처리를 해줘야함)

   ##### 2-1. throws를 쓰는 이유

    - 예외를 다 처리하게되면 중복 코드가 발생한다.
       - 한곳에 몰아서 예외를 다 처리하는 형태

```java
public void bb(int i) throws xxxException, xxxException{
   					 //throws 뒤에 쓴 예외는 던지고 호출 
    				 // 결국 다른 class에서 try catch문을 써줘야한다.
  //예외가 발생될 수 있는 구문이 속한 메소드에서 다시 예외를 전달하는
      //상위 메소드로 예외처리를 미루는 방법
}
```



3. 예외를 **강제**로 발생시켜라 =>throw

```java
XXXException e = new XXXException();  //예외 객체를 생성
throw e;  //프로그램 중지
```



4. 사용자 정의 Exception

- 필요에 의해서 우리가 만들어서 사용
- 비체크 체크중에 선택해서 XXXException을 상속받는다.

```java
class XXXException extends {
    throw new XXXException();
}
```



### 중첩클래스

```java
class A{	//outer클래스
    * inner의 형태
        1. 인스턴스 inner
        2. static inner
        3. 로컬 inner
    class B{	//inner클래스 - outer클래스쪽의 모든 속성과 메소드 접근
    }
}
//외부에서 A 없이는 B를 사용할 수 없다.
```

### inner클래스 예제

```java
/**
 * 	-Inner클래스의 형태 정리 - 선언 위치에 따라 3가지 정리
 * 	1. 인스턴스 멤버클래스
 * 	2. 정적(static) 멤버클래스
 * 	3. 로컬 클래스(메소드 내부에서 선언 - 멤버 안붙임)
*/
class Test{		//public or 생략
	int a=50;
	static int b=10;
	
	public void testMethod( ) { }
	public static void testMethod2( ) { }
	/**
	 * 	1. 인스턴스 멤버클래스 
	 * 	: 인스턴스 멤버클래스안에서는 static변수, static메소드 모두 접근 가능
	 * 	: 인스턴스 멤버클래스안에서는 static변수, static메소드 선언 안됨!
	 * 	: Outer클래스를 먼저 생성해야만 인스턴스멤버클래스를 사용할 수 있다.
	 * 	:  인스턴스 멤버클래스는 access modifier 모두 선언 가능
	 * 	:  ~.class 생성될 때 -> Outer클래스이름$Inner클래스 이름.class로 생성된다.  			-Test$InstanceInner.class
	 * */
	class InstanceInner{   //protected or private or public or 생략
		//속성과 메소드를 선언 할 수 있음
		int a =100;
		//static int b=50;  //선언 안됨
		public void aa( ) {
			System.out.println(a);		//100
			System.out.println(this.a);		//100  //Inner클래스의 a객체 호출
			System.out.println(Test.this.a);//50  //Outer클래스의 a객체 호출
			System.out.println(b);	 //10
			
			testMethod();
			testMethod2();
		}
		//public static void bb( ) { }  //선언 안됨
	}//InstanceInner끝
	
/**
 * 	2. 정적(static) 멤버클래스
 * 	: 외부에서 Outer클래스 생성없이 바로 접근 가능!
 * 	: static변수, non-static변수, static메소드, non-static메소드 모두 선언 가능
 * 	: Outer쪽의 static만 접근 가능(non-static 접근 불가)
 * 	: 클래스 앞에 access Modifier 모두 가능
 * */
	static class StaticInner{    //protected or private or public or 생략
			int a = 10;
			static String name = "장희정";
			
			public void aa( ) { 
				System.out.println(a);	
				System.out.println(name);	
				System.out.println(b);	
				
		//System.out.println(Test.this.a); //a가 static이 아니기 때문에 불가
				
				//testMethod();	//testMethod()가 static이 아니기 때문에 불가
				testMethod2();
			}
			public static void bb( ) { }
	}//StaticInner끝
	
	/**
	 *		 3. 로컬 클래스(메소드 내부에서 선언 - 멤버 안붙임)
	 *				: 로컬 클래스 앞에는 static, 접근제한자
	 				  (public, private, protected등등) 모두 안됨!!!
	 *				: Outer쪽의 static, non-static 접근은 가능
	 *				:
	 * */
		public void method() {
			class LocalClass{
				/*static*/  int sun =8;
				public void aa() {
					System.out.println(a);	 //50     //Outer쪽의 변수
					System.out.println(b);	 //10     //Outer쪽의 변수
				}
			}//LocalClass끝
			LocalClass local = new LocalClass();
			local.aa();
		}
}//Test 끝

public class InnerAccessExam {

	public static void main(String[] args) {
		    //	1)Instance 멤버 클래스 호출
			Test t = new Test();
			Test.InstanceInner innerInstance = t.new InstanceInner();
			innerInstance.aa();
			
			System.out.println("-----------------------------------------");
			//	2)정적멤버 클래스 호출
			Test.StaticInner st = new Test.StaticInner();
			st.aa();
			
			System.out.println("3) Local 클래스----------------------");
			//  3)Local클래스
			Test t3 = new Test();
			t3.method();
	}
}

```

