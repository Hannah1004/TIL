# 0910공부 -interface

### interface

```java
interface A{   }		//class대신해서 interface를 적어준다.
```

- class와 유사하지만 class는 아니다.(상속X, 생성X)
- interface를 구현(implements)하여 **다중 상속 같은 효과를 얻음**
- 생성할 수 없지만 변수(자료형-Type)로 사용가능
- class가 interface를 implements하게 되면 **interface에 있는 모든 method재정의를 해야한다.**
- 소스가 길어진다는 단점이 있음 - 1개만 사용하고 싶어도 모든 메소드를 재정의 해야하기 때문

- 인터페이스는 상수 필드만 선언가능
- 상수명은 대문자로 작성
- 선언과 동시에 초기값 지정

