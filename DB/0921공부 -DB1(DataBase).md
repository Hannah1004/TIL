# 0921공부 -DB(DataBase)

#### DB ->Oracle 11g download

##### DML : commit or rollback을 이용해서 저장, 취소가 가능하다.

### CRUD작업

1. **Create 문장** -> 테이블 생성(DDL)

   ```sql
   CREATE TABLE 테이블명(
   	NO NUMBER(2) PRIMARY KEY,
       Name VARCHAR(30) NOT NULL,
       Day DATE
       등등
   );
   ```

2. **Insert 문장** -> 레코드추가(삽입)(DML)

   ```sql
   INSERT INTO 테이블명 VALUES('3',' sql','2018-09-21');  =>모든 컬럼 삽입
   INSERT INTO 테이블명(NO,Name) VALUES('3',' sql'); => 원하는 컬럼만 삽입
   ```

3. **Update 문장** -> 레코드 수정(DML)

   ```sql
   UPDATE 테이블명 SET Name(컬럼명) = 'DB' WHERE NO='3';
   --> No가 3인 튜플의 Name을 DB로 수정
   ```

4. **Delete 문장** -> 레코드 삭제(DML)

   ```sql
   DELETE FROM 테이블명 WHERE 조건; => 조건의 행을 삭제
   DELETE FROM 테이블명; => 테이블의 모든 행 삭제
   --> 테이블의 모든 행을 삭제해도 테이블 구조는 살아있다.
   
   truncate table 테이블 이름; -- 모든 레코드 삭제(rollback안됨)
   ```

5. **Select 문장** -> 레코드 검색(DML)

   ```sql
   SELECT Name,Day(컬럼명) FROM 테이블명;
   select name as 이름, day 날짜 from 테이블명;
   --name을 이름으로 컬럼명을 바꿔서 보여주겠다.(실제로 바뀌지X)
   select distinct day from 테이블명;
   --day의 중복된 행을 제거하고 검색해준다.
   ```

6. **Drop 문장** ->테이블 삭제

   ```sql
   drop table 테이블명;
   ```

7. **Alert 문장** -> 테이블 변경

   1. 컬럼추가

      ```sql
      alter table 테이블이름 add 컬럼명 데이터타입 [제약 조건],...;
      ```

   2. 컬럼 삭제

      ```sql
      alter table 테이블이름 drop column 컬럼명;
      ```

   3. 데이터 타입 변경

      ```sql
      alter table 테이블이름 modify 컬럼명 변경데이터타입;
      ```

   4. 제약조건을 추가

      ```sql
      alter table 테이블이름 add constraint 별칭 제약조건;
      ex)
      alter table 테이블이름 add constraint aaa unique(no)
      ```

   5. 제약조건 삭제

      ```sql
      alter table 테이블이름 drop constraint 별칭;
      ```

   6. 컬럼 이름 변경

      ```sql
      alter table 테이블이름 rename column 기존컬럼명 to 변경컬럼명;
      ```


<hr>

### DataType 종류

1. **문자형**
   -  char(byte수), nchar(byte수, 유니코드 지원)
     - char만 써도 됨 ()안써도 되는데 1을 default로 하고 있음
   - varchar2(byte수), nvarchar(byte수, 유니코드 지원)
     - varchar2는 ()안에 숫자 꼭 써줘야한다.(생략 안됨)
     - varchar2(5 char) -- byte가 아니고 글자수
     - 4000byte 까지 가능
     - **반드시 *'  '* 묶는다.**   "  "는 안된다.

2. **숫자형**
   - number(자리수)
   - number(전체 자리수, 소수점 자리) : 실수형
   - int  => number(38) , number로 인식한다.
   - smallint  => number(38), number로 인식한다.
3. **날짜형**
   - date
     - '년-월-일' or '년/월/일' 사용
     - 현재 날짜와 시간 설정 : sysdate  <= ' '로 묶어서 쓰면 안됨

<hr>

### 제약조건 종류(5가지)

1. **Primary Key(기본키=대표키)**

   - 중복안되고 not null임

   - 자동으로 Index가 설정됨(검색 속도가 빠르다.)

   - 하나의 테이블에 기본키는 반드시 한개만 존재

   - 여러개의 컬럼을 묶어서 하나의 pk는 가능하다.

     ```sql
     constraint member_id_jumin_pk primary key(id, jumin)
     --> create문장 맨아래에 작성해야함
     --> pk하고 싶은 칼럼명을 여러개 써줄 수 있다.
     ```

2. **Foreign** **Key**

   - 다른 테이블의 기본키를 참조하는 키

   - 중복가능/ null허용

   - 참조되고 있는 테이블의 데이터 값 이외의 값은 삽입할 수 없다.

   - 한 테이블에 여러개의 컬림이 FK설정이 가능하다

   - insert할 때 부모를 insert하고 => 자식을 insert해야한다.

   - delete할 때 자식을 delete하고 => 부모를 insert해야한다.

   - 만약, fk생성할 때 on delete cascade 설정하면 

     부모가 삭제 될때 자동으로 자식도 삭제된다.

     ```sql
     ex)
     칼럼명 number(3) constraint no_fk references 테이블명(칼럼명) on delete cascade
     --을 쓰면 자동으로 부모와 자식의 칼럼이 삭제 된다.
     ```

   - 부모와 자식의 연결 칼럼명은 달라도 되지만 **datatype은 반드시 같아**야한다.

3. **Unique**

   - 중복 안됨(유일한 값), null허용(만약 not null지정해주면 null허용 안됨)
     - null은 중복이 가능하다.(값이 아니기 때문)
   - 테이블을 만들 때 pk와 같은 효과를 주기위한 제약조건
   - 한 테이블에 여러 컬럼을 사용가능 함
   - 대표키는 될 수 없는데 중복허용 안하고 싶을 때 사용

4. **Check**

   - 조건을 주어 조건에 만족하는 값만 삽입 가능하도록 하는 것

   - 조건을 설정하여 insert할 때 조건 이외의 값은 insert할 수 없도록 하는 것

     ```sql
     컬럼명 데이터타입 check (조건);
     ```

5. **default**

   - 기본값을 지정하여 값을 넣지 않아도 자동으로 기본값이 들어가도록 함

   - null을 허용했을 때 default컬럼의 값을 생략하면 무조건 default가 들어감

   - null을 입력하고 싶을 때는 직접 null을 넣어야 null이 들어감

     ```sql
     컬럼명 데이터타입 default 'aa'
     --컬럼명의 data를 주지않으면 default로 aa가 작성된다.
     ```

