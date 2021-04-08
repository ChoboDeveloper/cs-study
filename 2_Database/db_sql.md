# SQL

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

