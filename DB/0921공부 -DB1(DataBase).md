# 0921공부 -DB(DataBase)

#### DB ->Oracle 11g download

### 제약조건(5가지) -CRUD작업

1. Create 문장 -> 테이블 생성(DDL)

   ```sql
   CREATE TABLE 테이블명(
   	NO NUMBER(2) PRIMARY KEY,
       Name VARCHAR(30) NOT NULL,
       Day DATE
       등등
   );
   ```

2. Insert 문장 -> 레코드추가(삽입)(DML)

   ```sql
   INSERT INTO 테이블명 VALUES('3',' sql','2018-09-21');  =>모든 컬럼 삽입
   INSERT INTO 테이블명(NO,Name) VALUES('3',' sql'); => 원하는 컬럼만 삽입
   ```

3. Update 문장 -> 레코드 수정(DML)

   ```sql
   UPDATE 테이블명 SET Name(컬럼명); = 'DB' WHERE NO='3'
   => No가 3인 튜플의 Name을 DB로 수정
   ```

4. Delete 문장 -> 레코드 삭제(DML)

   ```sql
   DELETE FROM 테이블명 WHERE 조건; => 조건의 행을 삭제
   DELETE FROM 테이블명; => 테이블의 모든 행 삭제
   => 테이블의 모든 행을 삭제해도 테이블 구조는 살아있다.
   ```

5. Select 문장 -> 레코드 검색(DML)

   ```sql
   SELECT Name,Day(컬럼명) FROM 테이블명;
   ```

6. Drop 문장 ->테이블 삭제

   ```sql
   drop table 테이블명;
   ```


<hr>



### DataType 종류

1. 문자형
   -  char(byte수), nchar(byte수, 유니코드 지원)
     - char만 써도 됨 ()안써도 되는데 1을 default로 하고 있음
   - varchar2(byte수), nvarchar(byte수, 유니코드 지원)
     - varchar2는 ()안에 숫자 꼭 써줘야한다.(생략 안됨)
     - varchar2(5 char) -- byte가 아니고 글자수
     - 4000byte 까지 가능
     - 반드시 **'  '**묶는다.   "  "는 안된다.

2. 숫자형
   - number(자리수)
   - number(전체 자리수, 소수점 자리) : 실수형
   - int  => number(38) , number로 인식한다.
   - smallint  => number(38), number로 인식한다.
3. 날짜형
   - date
     - '년-월-일' or '년/월/일' 사용
     - 현재 날짜와 시간 설정 : sysdate

### 제약조건 종류

1. Primary Key(기본키=대표키)
   - 중복안되고 not null임
   - 자동으로 Index가 설정됨(검색 속도가 빠르다.)
   - 하나의 테이블에 기본키는 반드시 한개만 존재
   - 여러개의 컬럼을 묶어서 하나의 pk는 가능하다
2. 



