# DAY 11. 
---
## DataBase
* JDBC(Java DataBase Connectivity)
  * 자바와 DB를 연동하는 기술
  * DB 종류와 무관하게 연동 가능
  * SQLException 예외가 발생
    반드시 try~catch로, 또는 throws로 예외처리가 필요함


#### Database ve DBMS
* Database
  개인, 회사, 관공서 등에서 업무적으로 필요한 데이터
  사원 정보, 부서 정보 등등

* DBMS(DataBase Management System)
  DB를 전문적이고 효율적으로 관리하기 위한 S/W
  MySQL, Oracle, MS-SQL 등

---
#### DB의 종류
* 관계형 DB
* 계층형 DB
* 망형 DB
* 객체지향 DB

### 관계형 DB (Relational DataBase)
* 행 / 열로 구성된 2차원 테이블 형태를 가짐
* 여러 테이블 간에 특정 연결고리를 이용해서 관계를 맺어 관리됨
* MySQL, Oracle, MS-SQL, DB2등등

> 현업에서 RDB 데이터 구조를 가진 형태: **NoSQL (Not only SQL), Key:Value 구조**
> MongoDB, Cassandra
> {key: { key: {key : ...}}}
> 무한히 확장될 수 있는 특징을 갖고있다.


## SQL
* RDB에서 사용하는 언어
* 식별자로 구성 (예약어 및 사용자 지정 식별자 가능)
* 대·소문자 구별 안함 (SELECT 와 select는 동일함)
  * MySQL에서는 데이터에의 대소문자도 구분하지 않음. 
  * Oracle은 구분함

* 문자와 문자열 구분 또한 하지 않는다 ('A', "A")
  * 주로 홑따움표('')를 쓰도록 해라. 쌍따움표("")는 별칭(alias)에서만 사용하도록

* 산술연산자 및 연산자, 함수, 조건문

### SQL 문 종류
###### DB 종류에 따라
*주로 함수에서 차이가 있다*
* 표준화된 SQL (독립적인 SQL, ANSI SQL)
  * 모든 RDBMS에서 사용 가능
  
* 벤더(업체)에 의존적인 SQL문
  * MySQL에서만 사용
  * Oracle에서만 사용

###### 문법에 따라
1. DML (데이터 조작어, Data Manipulation Language)
   * INSERT, DELETE, UPDATE
2. DDL (데이터 정의어, Data Definition Language)
   * CREATE, ALTER, DROP, TURNCATE
3. TCL (트랜잭션 관리, Transaction Control Language)
   * COMMIT, ROLLBACK
4. DQL (Data Query Language)
   * SELECT
  
<pre>
///////
CRUD 작업 이란
    Create  : 생성
    Read    : 조회 (select)
    Update  : 수정 
    Delete  : 삭제
///////
</pre>
---
## select 문
*테이블 조회*
###### 기능
    selection   : 행(레코드)단위 검색
    projection  : 열(컬럼)단위 검색
    join        : 2개 이상의 테이블을 연결해서 원하는 데이터 조회


### null 값
값이 없는 데이터
* 기본적으로 모든 컬럼은 null을 가질 수 있음
  강제적으로 null을 갖지 못하도록 제한할 수 있음(NOT NULL)

---
### 제약 조건
1. Primary key(PK): 기본 키
   * 지정된 컬럼은 중복이 불가. 유일한 값을 가짐
   * 테이블 당 한개씩 지정 가능
   * 레코드를 식별하기 위해 사용
   * 복합 컬럼으로 지정 가능
   * 자동으로 index 생성
     *index 활용 시 원하는 record에 빠르게 접근할 수 있다* : 복합컬럼도 한개의 index로 생성
#####
    Index란
    특정 컬럼 값을 기준으로 B-트리(Balance Tree)를 생성
    트리를 기준으로 탐색을 하기 때문에 O(NlogN) 으로 빠르게 탐색이 가능
    있는 것과 없는 것에서 조회 속도 차이가 크다

    하지만, 트리의 구조가 바뀔만한 데이터의 변경이 발생할 경우 (내부적으로 정렬 or B트리 추가 작업)
    오히려 더 큰 오버헤드, 작업이 발생할 수 있으니 주의가 필요
2. unique *unique key (X)*
   * 지정된 컬럼은 반드시 **유일한** 값을 가짐. null 값도 가질 수 있음
   * 테이블당 여러개 지정 가능
   * 복합컬럼 가능
   * 자동으로 index 생성됨
  
3. check 
   * 비즈니스 로직 관련 제약 조건
#####
    ex) 성별: 남/여
        F/M, Female/Male, 1/0  이런식으로 가능할때
        1/0 <== 이것만으로 사용을 강제하는 제약조건
        
        학년: 1/2/3/4 
        등등

4. foreign key(fk)
   * 참조키 또는 외래키 제약조건
   * Join에 사용됨
   * 참조하는 pk와 fk의 컬럼 명이 굳이 같을 필요는 없다.
#####
    table1.fk > table2.pk
    table1: slave(child) table
    table2: master(parents) table
    slave table의 foreign key는 master table의 pk 또는 unique 컬럼만 참조가 가능.
    그리고 참조하는 컬럼이 가진 값 + null 값만을 가질 수 있다.

5. not null
   * null 값을 허용하지 않는 제약 조건
   * 테이블당 여러개 지정이 가능
   * *다른 제약조건과 다르게 **허용된 기능**을 제한하는 방식*
   * 다른 네가지 제약조건과 다르게 컬럼 레벨만 가능 (다른 애들은 테이블 레벨로도 설정이 가능)



   