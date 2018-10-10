# ex1010공부 -PL_SQL

### : 절차적 언어(선언, 변수, 실행부, 제어문, 함수, 프로시져...)

- #### 기본 구조

  ```SQL
  DECLARE 변수 선언;
  BEGIN
  	실행 문장;
  	DBMS_OUTPUT.PUT('PL_SQL');
  END;
  ```

- #### 변수 선언 방법

  - 변수이름 데이터 타입;

  - 데이터 타입의 종류

    - VARCHAR2, CHAR, NUMBER, DATE
    - 테이블이름.필드명%TYPE
    - 테이블이름%ROWTYPE

    ```SQL
    DECLARE 변수이름 타입;
    DECLARE 변수이름 := 초기값;
    DECLARE 변수이름 타입 DEFAULT 초기값;
    ```

  - 예시

  ```SQL
  DECLARE 
      NAME VARCHAR(20) :='이한나';
      AGE NUMBER(3) DEFAULT 23;
      ADDR VARCHAR2(50);
  BEGIN
      DBMS_OUTPUT.PUT_LINE('이름  :  '  || NAME);
      DBMS_OUTPUT.PUT_LINE('나이  :  '  || AGE);
      DBMS_OUTPUT.PUT_LINE('주소  :  '  || ADDR);
  END;
  ---------------------결과-----------------------
  이름  :  이한나
  나이  :  23
  주소  :         --주소에 값을 안줘서 값이 나오지 않는다.
  ```

  - 예시

  ```SQL
  --EX) EMP테이블에서 EMPNO가 7369인 사원의 이름과 급여 출력
  --(출력 : ~님의 급여정보는 ~입니다.)
  DECLARE
      E_ENAME EMP.ENAME%TYPE;
      E_SAL EMP.SAL%TYPE;
  BEGIN
      SELECT ENAME, SAL INTO E_ENAME, E_SAL FROM EMP WHERE EMPNO=7369;
      DBMS_OUTPUT.PUT_LINE(E_ENAME || '님의 급여정보는 ' || E_SAL || '입니다.');
  END;
  
  --EX)EMP 테이블에서 EMPNO가 7369인 사원의 모든 정보 출력
  DECLARE
      DATA EMP%ROWTYPE;
  BEGIN
      SELECT * INTO DATA FROM EMP WHERE EMPNO=7369;
      DBMS_OUTPUT.PUT_LINE(DATA.EMPNO  || ' ' || DATA.ENAME|| ' '  || DATA.JOB );
  END;
  ```

  <HR>

- #### EXCEPTION

  ```SQL
  EXCEPTION
  	WHEN  예외종류 THEN 예외발생했을 때 실행문장;
  	WHEN  예외종류 THEN 예외발생했을 때 실행문장;
  	WHEN  예외종류 THEN 예외발생했을 때 실행문장;
  	...
  	WHEN  예외종류 THEN 예외발생했을 때 실행문장;
  ```

  - 예시

  ```SQL
  DECLARE
      COUNTER NUMBER(3)  :=100;
  BEGIN
      COUNTER :=COUNTER/0;
      DBMS_OUTPUT.PUT_LINE(COUNTER);
      EXCEPTION  --예외가 발생했을 때만 실행된다.
          WHEN ZERO_DIVIDE THEN 
          	DBMS_OUTPUT.PUT_LINE('예외가 발생했어요  ');
              DBMS_OUTPUT.PUT_LINE('0으로 나눌수 없습니다.');
  END;
  ```

  <HR>

- #### 조건문

  - IF문

  ```SQL
  IF 조건식 THEN 실행문장;
       ELSIF 조건식 THEN 실행문장;
       ELSIF 조건식 THEN 실행문장;
       ....
       ELSE 실행문장;
       END IF;
  --------------예시-----------------------
  DECLARE
      NO NUMBER(3) :=60;
  BEGIN
      IF MOD(NO, 2)=0 THEN  DBMS_OUTPUT.PUT_LINE(NO || '는 짝수');
      ELSE  DBMS_OUTPUT.PUT_LINE(NO || '는 홀수');
      END IF;
  END;
  ```

  - CASE문

  ```SQL
   case 대상
     when 값 then 실행문장;
     when 값 then 실행문장;
     when 값 then 실행문장;
     else 실행문장;
   end case;
  -------------예시----------------
  --------------------------------------------------------------
  DECLARE
      NO NUMBER(3) :=60;
  BEGIN
      CASE 
          WHEN MOD(NO, 2)=0 THEN  DBMS_OUTPUT.PUT_LINE(NO || '는 짝수');
          ELSE  DBMS_OUTPUT.PUT_LINE(NO || '는 홀수');
      END CASE;
  END;
  ```

  <HR>

- #### 반복문

  - FOR문

  ```sql
  --FOR문
  FOR 변수이름 [REVERSE] IN 시작  ...끝 LOOP
  	실행문장
  END LOOP;
  --------------예시----------------------
  BEGIN
      FOR  i  IN 1 .. 10 LOOP
          DBMS_OUTPUT.PUT_LINE(i);        
      END LOOP;
  END;
  ```

  - LOOP END문

  ```SQL
  --LOOP END문
  LOOP
  	실행문장,
  	증감식
  	[EXIT WHEN 조건식]  --반복문을 빠져나가라.
  END LOOP;
  --------------예시------------------------
  DECLARE I NUMBER(3) := 1;
  BEGIN
      LOOP
          DBMS_OUTPUT.PUT_LINE (I);
              I := I + 1;
              EXIT WHEN I=11;
      END LOOP;
  END;
  ```

  - WHILE문

  ```SQL
  --WHILE문
  WHILE 조건식 LOOP
  	실행문장;
  	증감식;
  END LOOP;
  ------예시-------
  DECLARE I NUMBER(3) := 1;
  BEGIN  
      WHILE I<11 LOOP
          DBMS_OUTPUT.PUT_LINE (I);
              I := I + 1;
      END LOOP;
  END;
  ```

  <HR>

- #### CURSOR

  - SELECT의 결과집합이 여러개의 레코드를 반환할 때 사용한다.

  - 커서 사용방법

    ```SQL
    1)선언
    	CURSOR 커서이름 IS SELECT 문장; --DECLARE 위치에 선언한다.
    2)열기
    	OPEN 커서이름;
    3)데이터 가져오기
    	FETCH 커서이름 INTO 변수이름, ,,,; --반복문안에서 
    4)닫기
    	CLOSE 커서이름;
    ```
