# SQL

<br>

### Assertion

* relation의 어떠한 change라도 발생하면 그 즉시 발동된다.
* CHECK는 선언되고 나타난 그 Relation안에서 참조를 하는 거라면, ASSERTION은 독립적으로 생성하여 어떤 Column이든 상관없이 수행한다.
* Trigger은 삽입이나 갱신과 같은 이벤트에 명시하는 제약조건이라면, ASSERTION은 해당 릴레이션에 대한 지속적인 제약조건을 의미한다.

---

#### ON DELETE

* CASCADE
  * 참조되는 테이블에서 데이터를 삭제하거나 수정하면,  참조하는 테이블에서도 삭제와 수정이 일어난다.
* SET NULL
* NO ACTION
  * 명시적으로 프로그램에서 자식 테이블의 Row 모두 삭제하고 부모 테이블의 Row를 삭제해야됨
* SET DEFAULT

---

### 조건연산자

* CHECK
  * 입력값을 제한한다. CHECK([조건절])

---

### GROUP BY

* GROUP BY 뒤의 변수 제외하고는 일반행을 SELECT 할 수 없다.

```sql
SELECT ID, COUNT(FIRST_CAT), MAX(NUMS)
FROM sql_test_b
Group BY ID;
```

* GROUP BY는 NULL까지 포함

* **NVL(COLUMN, 표시할값)** 
  * 조건에서 NULL을 뺄건지 말건지를 지정해주어야한다.
  * 만약, NULL이 의미가 있다면 제외를 하면 안되겠지만, 'NULL이라고 보여주기 싫다면 ~~라고 처리해라' 라고 할 수 있는 함수가 NVL

```sql
-- NVL 함수는 값이 NULL인 경우 지정값을 출력하고, NULL이 아니면 원래 값을 그대로 출력한다.
-- 함수  :  NVL("값", "지정값")

-- 부서별 가장 높은 연봉과 가장 낮은 연봉
-- 부서별 전체 연봉의 합, 전체 연봉의 평균을 구하시오.
SELECT NVL(DEPARTMENT_ID, 0)
        , MAX(SALARY)
        , MIN(SALARY)
        , SUM(SALARY)
        , ROUND(AVG(SALARY))
FROM    EMPLOYEES
GROUP   BY DEPARTMENT_ID
ORDER   BY DEPARTMENT_ID
;
```



---

### ORDER BY

* ASC(기본값)
* DESC

---

### NULL

* NULL에 대한 산술연산의 결과는 NULL이다
  * NULL + 100 = NULL

---

### 집합연산자

* UNION
* UNION ALL
  * UNION과의 차이점은, 중복된 항목도 모두 조회한다는 것
* INTERSECT
  * 교집합
* MINUS
  * 차집합

---

### 관계대수

* 순수 관계 연산자
  * SELECT, PROJECT, DIVISION, JOIN
* 일반 집합 연산자
  * UNION, INTERSECT, MINUS

* 완전집합
  * 연산자 집합 ![image](https://user-images.githubusercontent.com/75229881/164007076-5d958e9a-561a-4f1d-a100-2514a4296c33.png)를 관계대수 연산자의 **완전 집합(complete set)**이라 부른다.
  * 이 연산자 집합과 동등한 모든 질의 언어들은 **관계적으로 완전하다(relationally complete)**라고 정의한다.

<br>

* SELECT
  * 단항 연산으로 릴레이션에서 조건에 맞는 레코드를 분리해내는 연산
* PROJECT
  * 단항 연산으로 릴레이션에서 참조하고자 하는 어트리뷰트를 선택하여 분리해 내는 연산
* JOIN
  * 두 개 이상의 릴레이션에서 조건에 맞는 튜플이나 어플리뷰트를 조합하여 새로운 릴레이션을 생성하는 연산
* DIVISION
  * 두 개의 릴레이션 A와 B가 있을 때 B의 릴레이션의 모든 조건을 만족하는 경우의 튜플들을 릴레이션 A에서 분리해 내어 프로젝션하는 연산

---

### JOIN

**비동등 조인**

* 두 개의 테이블 간에 칼럼 값들이 서로 정확하게 일치하지 않는 경우에 사용된다. 
* 비동등조인의 경우 '=' 연산자가 아닌 다른 (Between, >, >=, <, <= 등) 연산자들을 사용하여 JOIN을 수행하는 것이다.
* 예제

```sql
SELECT E.ENAME, E.JOB, E.SAL, S.GRADE

FROM EMP E, SALGRADE S

WHERE E.SAL BETWEEN S.LOSAL AND S.HISAL;
```

![image](https://user-images.githubusercontent.com/75229881/164010895-ea8a865c-c14e-4028-9155-220a474024a3.png)

![img](https://t1.daumcdn.net/cfile/tistory/2253A64B57B5920D28)

* 비동등조인은 Cartesian Product 현상 발생여부를 충분히 고려한 뒤 사용해야 한다

<Br>

**외부조인**

![image](https://user-images.githubusercontent.com/75229881/164446402-ab175d53-c1cb-4e5d-9d68-9f8b5ca937f8.png)

* 상대 릴레이션에서 대응되는 튜플을 갖지 못하는 튜플이나 조인 애트리뷰트에 널 값이 들어 있는 튜플들을 다루기 위해서 조인 연산을 확장한 것
* 두 릴레이션에서 대응되는 튜플들을 결합하면서 대응되는 튜플을 갖지 않는 튜플과 조인 애트리뷰트에 널 값을 갖는 튜플도 결과에 포함한다.
* **LEFT, RIGHT는 살리는 쪽임**
* 한 릴레이션에 있는 튜플이 조인할 상대 릴레이션에 대응하는 튜플이 없는 경우, 상대를 Null 튜플로 만들어 결과에 포함
* 두 조인 릴레이션의 모든 튜플들이 결과 릴레이션에 포함됨

<br>

**세미조인**

* 조인 대상 릴레이션 중 하나를 프로젝트(PROJECT) 연산을 수행한 후 조인을 하는 것

![image](https://user-images.githubusercontent.com/75229881/164446471-9411b289-9349-41e6-a478-cb73b6716ef0.png)

<br>

**세타조인**

* 조인에 참여하는 두 릴레이션의 속성 값을 비교하여 조건을 만족하는 투플만 반환한다.
* 세타조인의 조건은{=,≠,≥,≤,>,<} 중 하나가 된다.
* 세타조인 중 특별히 비교연산자가 = 인 경우 **동등조인(equi join)**, 동등조인에서 **중복속성이 제거**된 것이 바로 **자연조인(natrual join)**
  * 자연조인에서 **중복 속성이지 중복 튜블 아님!**


---

### 질의 최적화

**불필요한 Sort 방지**

>  [구루비 DB 스터디 - 개발자, DBA가 함께 만들어가는 구루비 지식창고! (gurubee.net)](http://wiki.gurubee.net/pages/viewpage.action?pageId=26742238)

* UNION ALL 보다는 UNION
* Dinstinct 보다는 Exist Sub Query
* Sort Unique 보다는 Sort Aggregate
* 데이터 존재여부 확인 시 불필요한 Count 제거

---

### DISTINCT

**NULL 포함 여부**

* 포함되는 경우 : COUNT**(\*)**
* 포함되지 않는 경우: COUNT**(ColumnName)**
* COUNT( DISTINCT( ColumnName ) )으로 하면 중복되지 않고 NULL은 제외되는 값들만 COUNT

---

