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



---
