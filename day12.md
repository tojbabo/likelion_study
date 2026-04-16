# DAY 12.
---
## 조인(Join)
**2개 이상의 table에서 selection과 projection을 처리하는 것**
selection : 레코드 선택 - where
projection : 컬럼 선택 - select

-- 원하는 데이터가 여러 테이블에 분산되어 있는 경우 사용
=> 테이블 연결하는 것

inner 조인 - 테이블 간에 연결이 되는 데이터만 출력
outter 조인 - 누락된 데이터까지 포함해서 출력

equi 조인 - 정확하게 일치하는 방식, 동등연사자 사용
non-equi조인 - 값이 정확하게 일치하지 않는 조인, 부등연산자 사용

###### cross 조인
    > select * from tableA cross join tableB
    tableA의 하나의 레코드가 tableB의 모든 레코드와 연결됨.
    조인된 결과는 데이터로서 사용은 불가
    tableA의 레코드 수 * tableB의 레코드 수 만큼 출력됨

###### natural 조인
    > select * from tableA natural join tableB
    tableA와 tableB의 공통컬럼을 찾아서 조인
    공통 컬럼이 두 개 이상일 경우, 모두 일치해야 조인
    공통 컬럼이 없으면 조인 안됨
    어떤 컬럼으로 조인됐는지는 직접 확인이 필요함. > 가독성이 떨어진다

**using(column) 키워드로 공통 컬럼을 지정할 수 이씀**
> select * from tableA inner join tableB using(name)
> 내부적으로 동등 연산자를 쓰는, inner join에 속함

**on 절: 좀 더 범용적이고 가독성이 좋다**
> select * from tableA inner join tableB on tableA.name = tableB.name
> 내부적으로 동등 연산자를 쓰는, inner join에 속함
>
> select * from a join b on a.sal between b.losal and b.hisal
> 이렇게 non-equi 조인을 할수도 있다


###### self 조인
*자신이 자신을 join 하는 방법*
    > select * from tableA natural join tabl

---
### subquery문
    ( )안에서 선언됨
    서브쿼리가 먼저 실행, 그 결과 값을 main query에서 실행
    거의 모든 곳에서 사용이 가능
    where, having, from, insert, delete, update, create ...

***복수행 연산자***
< > 단일행 연산자: = , >, >= 등등
*서브쿼리가 실행된 후 하나의 행을 리턴하는 경우 단일행 연산을 함*

**서브 쿼리의 결과가 복수행을 리턴하는 경우**
- IN, ANY, ALL EXSISTS : 복수행 연산자 사용

* 인라인뷰(Inline-view): 서브쿼리의 결과 테이블을 지칭

