# 0928공부 -DB3(JOIN, SUBQUERY 등등)

## JOIN 

- 한번의 SELECT문장으로 여러 테이블에 있는 컬럼의 정보를 검색할 때 사용한다.-- 

##### -- JOIN의 종류

1. INNER JOIN(EQ JOIN=동등조인)

   1. SQL 조인 방식

      - 주의 : 양쪽 테이블에 같은 이름의 컬럼이 있을 경우 반드시 테이블이름(별칭).컬럼명을 사용한다.

      ```SQL
      SELECT 컬럼명,...
      FROM 테이블이름 별칭, 테이블이름 별칭,....
      WHERE 조건식 AND 조건식.....
      ```

   2. ANSI 조인 방식(권장하는 방식)

      ```SQL
      SELECT 컬럼명,...
      FROM 테이블 이름 [INNER] JOIN 테이블 이름,....
      ON 조건식 AND 조건식 ....
      ```

      - USING 컬럼명 사용하기(ANSI에서만 가능)

      ```SQL
      SELECT 컬럼명,...
      FROM 테이블 이름 [INNER] JOIN 테이블 이름,....
      USING (겹치는 컬럼명) --양쪽테이블의 조건대상컬럼의 이름이 동일할 때만 사용가능
      --주의 : USING을 사용하면 SELECT절에 나오는 양쪽테이블의 동일한 이름은 반드시 컬럼명만 사용해야한다.
      EX) 테이블이름.컬럼명 안된다.
      ```

2. OUTER JOIN

   - LEFT JOIN - 왼쪽 테이블의 컬럼이 다 나온다.

     1. SQL 조인방식

     ```SQL
     SELECT T1.ID, NAME, JOB, SAL
     FROM TEST1 T1, TEST2 T2
     WHERE T1.ID = T2.ID(+);
     ```

     2. ANSI 조인방식

     ```SQL
     SELECT ID, NAME, JOB, SAL
     FROM TEST1 LEFT JOIN TEST2
     USING (ID);
     ```

   - RIGHT JOIN - 오른쪽 테이블의 컬럼이 다 나온다.

     1. SQL 조인방식

     ```SQL
     SELECT T1.ID, NAME, JOB, SAL
     FROM TEST1 T1, TEST2 T2
     WHERE T1.ID(+) = T2.ID;
     ```

     2. ANSI 조인방식

     ```SQL
     SELECT ID, NAME, JOB, SAL
     FROM TEST1 RIGHT JOIN TEST2
     USING (ID);
     ```

   - FULL JOIN - 모든 테이블의 컬럼이 다 나온다.

     1. **SQL 조인방식(지원하지 않는다.)**
     2. ANSI 조인방식

     ```SQL
     SELECT ID, NAME, JOB, SAL
     FROM TEST1 FULL JOIN TEST2
     USING (ID);
     ```

3. SELF JOIN : 하나의 테이블을 두개의 테이블처럼 사용하여 자기 자신테이블을 조인하는 것

   ​		     (재귀적관계일 때 사용)

   ```SQL
   SELECT E1.ENAME 사원이름 , E2.ENAME 상사이름
   FROM EMP E1, EMP E2 --E1을 사원TABLE, E2를 상사TABLE
   WHERE E1.MGR=E2.EMPNO;
   --사원TABLE에 MGR과 상사TABLE에 EMPNO가 같은지 비교해야한다.
   ```

<HR>

#### --3개 이상의 테이블을 JOIN할 때

1. SQL 조인방식

   ```SQL
   SELECT T1. ID, NAME, JOB, SAL, MANAGER_NAME
   FROM TEST1 T1, TEST2 T2, TEST3 T3
   WHERE T1.ID = T2.ID AND T2.CODE= T3.CODE;
   ```

2. ANSI 조인방식

   - USING방식

   ```SQL
   SELECT ID, NAME, JOB, SAL, MANAGER_NAME
   FROM TEST1 JOIN TEST2
   USING (ID) JOIN TEST3 USING(CODE);
   ```

   - ON 방식

   ```SQL
   SELECT TEST1.ID, NAME, JOB, SAL, MANAGER_NAME
   FROM TEST1 JOIN TEST2
   ON TEST1.ID = TEST2.ID JOIN TEST3 
   ON TEST2.CODE = TEST3.CODE;
   ```



## SET집합

- 반드시 열의 개수와 타입이 일치!!
- 열의 순서도 같아야한다.

1. UNION : 중복행을 제거한 합집합

   ```SQL
   SELECT 컬럼명, 컬럼명, ...
   FROM 테이블명
   UNION
   SELECT 컬럼명, 컬럼명, ... 
   FROM 테이블명
   ```

2. UNION ALL : 중복행을 포함한 합집합

   ```SQL
   SELECT 컬럼명, 컬럼명, ...
   FROM 테이블명
   UNION ALL
   SELECT 컬럼명, 컬럼명, ... 
   FROM 테이블명
   ```

3. INTERSECT : 교집합

   ```SQL
   SELECT 컬럼명, 컬럼명, ...
   FROM 테이블명
   INTERSECT
   SELECT 컬럼명, 컬럼명, ... 
   FROM 테이블명
   ```

4. MINUS : 차집합

   ```SQL
   SELECT 컬럼명, 컬럼명, ...
   FROM 테이블명
   MINUS
   SELECT 컬럼명, 컬럼명, ... 
   FROM 테이블명
   ```

------

## SUBQUERY

- 메인 쿼리 안에서 또 다른 쿼리문이 존재하는 것

- 반드시 서브쿼리를 괄호로 묶는다.

- 메인쿼리 보다 서브쿼리가 먼제 실행되어 결과를 메인 쿼리의 조건으로 사용한다.

- 서브쿼리의 결과가 한개 이상 반환될 때는 IN, ANY, ALL 연산자를 사용한다.

- 서브쿼리의 결과가 한개일 때는 비교연산자 사용한다.

  ```SQL
  SELECT * FROM EMP WHERE ENAME = (서브쿼리문장);
  ```

- 주로 SELECT에서 많이 사용하지만 UPDATE, DELETE, INSERT에서 사용가능하다.

  ```SQL
  --SUBQUERY를 이용한 INSERT
  INSERT INTO 테이블이름(서브쿼리)
  --SUBQUERY를 이용한 UPDATE
  UPDATE 테이블이름 SET 조건 = (서브쿼리) WHERE  ;
  --SUBQUERY를 이용한 DELETE
  DELETE 테이블이름  
  ```

- 인라인 뷰 : FROM 절에 나오는 SUBQUERY

  ```SQL
  SELECT ROWNUM,EMPNO, ENAME, JOB, SAL
  FROM (SELECT * FROM EMP ORDER BY SAL);
  ```


