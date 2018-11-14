# Spring FrameWork

### 라이브러리와 프레임 워크의 차이점 - 많이 물어보는 질문

- 라이브러리
  - 유저코드가 라이브러리를 호출
  - 독립적을 작성
  - 유저코드가 제어
- 프레임 워크
  - 프레임워크코드가 유저코드를 호출
  - 프레임워크가 제어
  - 프레임워크 클래스를 서브클래싱해서 작성

### 메이븐

- 라이브러리 관리 + 빌드 툴

- 프로젝트에 필요한 관련된 라이브러리를 관리해주는 것

- 필요한 라이브러리를 다운받아 필요한 것만 build path 해주면 됨

- #### maven기반의 Project Pachage구조

  - src/main/java - 모든 자바소스
  - src/main/resources - 설정문서 모아두기
  - src/test/java - 단위테스트할때 사용

<hr>

## Spring Framework의 특징

- java개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크이다.

1. ##### Spring DI(Dependency InJection) = IoC(Inversion of Control)

   - container로 부터 의존관계에 있는 것을 자동으로 넣어주는 것
   - 객체들의 라이프사이클을 관리해준다. - container
   - 객체와 객체간의 **결합도를 최대한 낮춘다.**
     - 유지보수할때 소스 변경이 적다.
   - setter로서의 주입
   - 생성자로서의 주입
   - DI 컨테이너가 관리하는 객체를 빈이라고한다.
   - 컨테이너 빈 팩토리 -> 빈들을 관리함

2. ##### Spring AOP(Aspect Oriented Programing)

   - 관점 지향 프로그램(servlet에서 filter와 비슷)
   - 공통기능을 빼고 praxy server을 이용해서 ubing해서 호출해서 쓴다.
   - 공통 기능과 핵심기능이 완전히 나뉘어져 있다.

3. ##### Spring Web MVC

4. ##### Spring ORM(Object Relation Mapping)->JDBC역할을 한다.

   - 객체 DB를 연결해주는 역할

5. ##### Spring Ajax

   - 화면의 새로고침 없이 화면을 갱신해준다.
   - 응답해주는 사이클이 jsp와 다르다.

6. ##### Spring  tranjection

7. ##### Spring tiles -> (view template)-jsp의 include와 비슷

   - 설정에 mapping시켜주면 된다.

8. ##### Spring Security

   - 인증(로그인)과 권한

9. ##### Spring POJO