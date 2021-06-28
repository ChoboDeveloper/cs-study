# 트랜잭션

<br>

### 트랜잭션 격리 수준

**Read Uncommited** : Dirty Read, Non-repeatable Read, Phantom Read 발생

**Read Committed** :  Dirty Read 방지 / Non-repeatable Read, Phantom Read 발생

**Repeatable Read** : Dirty Read, Non-repeatable Read 방지 / Phantom Read 발생

**Serializable** : Dirty Read, Non-repeatable Read, Phantom Read 방지

> Dirty Read : T1이 트랜잭션 도중 T2가 값을 읽었으나 Rollback이 일어나면 발생 (Read date Disappeared)
>
> Non-repeatable Read : T1이 데이터를 읽고 T2가 데이터를 쓰고(Update) T1이 다시 한번 데이터를 읽을 때 생기는 문제 (Read Data Changed)
>
> Phantom Read : T1이 데이터를 읽고 T2가 데이터를 쓰고(Insert) T1이 다시 한번 데이터를 읽을 때 생기는 문제, (Non-Read Data Inserted)

---

### 직렬성

**충돌 직렬성**

> 서로 다른 트랜잭션에서 동일한 자원에 대해 연속적으로 읽기/읽기를 제외한 쓰기가 하나라도 발생하면 충돌

* 각 트랜잭션에서 R1(x), W2(x)와 같이 연속적으로 동일 데이터에 접근했을 때 R,R을 제외하고 선행 그래프로 표현할 수 있다. 여기서 Cycle이 형성된 경우 충돌이 발생한 것이며, 충돌이 발생하지 않은 경우 충돌 직렬성을 가진다고 말한다.

**뷰 직렬성**

* 모든 충돌 직렬 스케줄은 뷰 직렬

* 충돌 직렬이 아니고 blind write인 경우(읽지 않고 쓰기) 뷰 직렬
* 모든 트랙잭션이 같은 값을 Read하면 뷰 직렬

---

### Locking 기법

**2단계 Locking**

> unlock 이후에 lock이 나올 수 없음

- 확장 단계(Growing Phase): 트랜잭션은 새로운 lock 연산만 할 수 있고, unlock 연산은 할 수 없는 단계
- 축소 단계(Shrinking Phase): 트랜잭션은 unlock 연산만 실행할 수 있고, lock 연산은 실행할 수 없는 단계

---

### 회복기법

**즉시/지연갱신**

* 즉시 갱신
  * 트랜잭션 수행 도중에도 변경 내용을 즉시 데이터베이스에 기록
  * 커밋 발생 이전의 갱신은 원자성이 보장되지 않는 미완료 갱신이므로 장애 발생 시 UNDO 필요

* 지연 갱신
  * 트랜잭션의 부분 완료 상태에선 변경 내용을 로그 파일에만 저장
  * 중간에 장애가 생기더라도 데이터베이스에 기록되지 않았으므로 UNDO가 필요 없음

**체크포인트**

* 검사점 이후 커밋은 Redo
* 즉시 갱신 시 검사점 이후 커밋이 없는 트랜잭션은 Undo

---

### 복구성

**연쇄 복구 스케줄**

* 하나의 트랜잭션이 취소됨으로써 쓴 값을 읽어간 일련의 트랜잭션들이 따라서 취소되는 현상
* 예를들어, S1에서 T1:W(A), T2:R(A),W(A) T3:R(A) 를 연속적으로 실행한경우 T1를 Rollback할 경우 T2, T3 연속으로 Rollback 되어야함. 

**비연쇄 스케줄**

* Ti에 의하여 쓰여진 하나의 자료 항목을 Tj가 읽는 한 쌍의 트랜잭션 Ti와 Tj 에서 Tj의 읽기 연산에 앞서 Ti의 완료 연산이 실행되는 스케줄

* 위의 경우와 달리 T1을 Commit한 경우, T1만 철회함으로 이를 해결 가능

**뷰 동치 스케줄**

* S1, S2는 같은 트랜잭션들을 포함해야함
* 각 트랜잭션은 같은 값을 Read 해야함
* 마지막 Write연산이 같아야함

---



