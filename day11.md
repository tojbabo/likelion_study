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
* null 값에 연산을 할 경우 null이 나온다
  따라서 기본 값을 임의의 값으로 설정해주는 것이 좋음
<pre>
    ifnull(컬럼명, 기본값) <=== 컬럼 값이 null일때 기본값으로 연산
                              orcle에서는 NVL(컬럼명, 기본값)

    ex) select num + 10 as numA, ifnull(num,20) + 10 from ...
</pre>
* is null / is not null 연산으로 찾기
* 정렬 시 null 값은 가장 최소값으로 처리 (oracle에서는 최대값)

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



---
* distinct 중복제거
* between A and B : A와 B범위의 존재하는 값을 찾음. A와 B값 포함
* IN (값 1, 값 2, 값3 ...)
select distinct a, b 
from t
where sal between '2025-06-20' and '2025-08-02' or name in ('a','b','c');


#### like 연선자
* 패턴(와일드 카드)으로 조회
* 와일드 카드
  * %: 없거나 여러개 값으로 치환
  * _: 반드시 하나의 값으로 치환

######
    select * from emp
    where name like '%A%';      // A가 포함된 이름
    where name like 'A%';       // A로 시작하는 이름
    where name like '%A';       // A로 끝나는 이름
    where name like '_A';       // 두글자이고 A로 끝나는 이름
    where name like '___A%';    // 네번째 글자가 A인 이름

--- 
## 함수

###### 문자열 함수
    lower()                       : 소문자
    upper()                       : 대문자

    CONCAT(str1,str2,str3 ...)    : 문자열 합치기
    CONCAT_WS(separator,str1,str2...) 
      : separator를 중간에 포함하는 문자열 합치기

    LPAD/ RPAD(str,len,padstr)    : 문자 채우기
    
    SUBSTIRNG/ SUBSTR(str,pos,len)     
      : 부분 문자열 (pos는 1부터 시작)
    RIGHT/ LEFT(str,len)
      : 왼쪽(오른쪽) len길이의 부분 문자열

    LENGTH(str), CHAR_LENGTH(str)
      : 문자열 길이

    REPLACE(str, fromstr, tostr)  : 문자열 바꾸기
    INSERT(str, pos, len, newstr) 

    INSTR(str, substr)            : 특정 문자열 위치 가져오기

    LTRIM/ RTRIM/ LRTRIM(str)     : 공백 제거

    TRIM(BOTH substr from str)    : 특정 문자 제거
    TRIM(LEADING substr from str) : 왼쪽에서 문자 제거
    TRIM(TRAINIG substr from str) : 오른쪽에서 문자 제거

    REPEAT(str, count)            : 문자열 반복

    REVERSE(str)                  : 문자열 뒤집기

    SPACE(n)                      : n 만큼의 공백 반환
    
    FORMAT(정수, 소수점자릿수 [,locale])
      : 정수값을 포맷을 가진 문자열로 출력(반올림)
      > FORMAT(1123.12345, 4) => "1,123.1235"
      > FORMAT(1123.12345, 4, 'ko_kr') => "1,123.1235" // 기본은 en_us


###### 숫자 함수
    ABS(n)              : 절대값
    SIGN(n)             : n이 양수면 1, 음수면 -1, 0이면 0
    ROUND(n, [m])       : 반올림, m 자릿수
    TRUNCATE(n, m)      : m자릿 수 아래 버림(반내림)
    ceil, floor         
      : 소숫점을 가진 값을 정수로 변경 (ceil: 보다 큰 정수, floor: 같거나 작은 정수)
    MOD(n,m)            : n을 m으로 나눈 나머지


###### 날짜 함수
    NOW(), current_timestamp()
      'YYYY-MM-DD hh:mm:ss': SQL 실행 시점의 현재시간
    SYSDATE()  
      'YYYY-MM-DD hh:mm:ss': 함수 호출 시점의 현재시간

    curdate(), current_date(), current_date 
      'YYYY-MM-DD': 현재 날짜 정보

    curtime(), cureent_time(), current_time
      'hh:mm:ss': 현재 시간

    adddate(date,day): 날짜 정보에 일 수 만큼 더함
    <> subdate(date, day)
    ++ date_add('2020-10-10', interval 31 month) <> date_sub('2020-10-10', interval 31 month)

    datediff(date1, date2): 두 날짜의 일 차이
    timestampdiff(unit, time1, tim2)
      : unit(year, month 등등)에 따른 두 시간 데이터 차이

    last_day(date): 오늘 날짜 기준 이번달 마지막 날 구하기

    extract(unit from now()): 지금 기준 unit 연월일 시분초 구하기

    date_format(date, format)
      format - '%Y-%M,%D': date to string
    
    str_to_date(str, format): string to date
      str_to_date('2026::10::31','%y::%m::%d')
    
###### 조건 함수
    if(exp, true result, false result): 조건문
      if(1 > 2, '정답', '오답') -> "오답"

    case: switch 문
      case name when 'A' then 1
                hwen 'b' then 2
                else 3
      end

      case when id > 10 then 1
           when id > 20 then 2
           else 3
      end

###### 형변환 함수
    cast(10 as char): 10 -> '10'

  
##### 그룹 함수
    sum(), avg(), max(), min(), count()
    distinct를 옵션으로 넣을 수 있다[sum(distinct point)]
    count()의 경우 기본적으로 null 값은 제외.
    
    group by 를 통해 그룹으로 묶는다
    having 을 통해 묶은 애들에 조건을 줌

    where과 having의 차이점. where은 묶기전 조건, having은 묶은 후 조건

    


