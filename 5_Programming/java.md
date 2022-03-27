# Java

<br>

### 추상클래스/인터페이스

> **추상클래스는 IS - A "~이다".**
>
> **인터페이스는 HAS - A "~을 할 수 있는".**

![image](https://user-images.githubusercontent.com/75229881/136740684-a9aa12cb-935a-42c4-9f5c-22e3358ecc98.png)

---

### Spring

**계층**

* **Presentation Layer**
  * 브라우저상의 웹 클라이언트의 요청 및 응답을 처리
  * 서비스계층, 데이터 엑세스 계층에서 발생하는 Exception을 처리
  * **@Controller 어노테이션**을 사용하여 작성된 Controller 클래스가 이 계층에 속함
* **Business Layer**
  * 애플리케이션 비즈니스 로직 처리와 비즈니스와 관련된 도메인 모델의 적합성 검증
  * 트랜잭션 관리
  * 프레젠테이션 계층과 데이터 엑세스 계층 사이를 연결하는 역할로서 두 계층이 직접적으로 통신하지 않게 함
  * Service 인터페이스와 **@Service 어노테이션**을 사용하여 작성된 Service 구현 클래스가 이 계층에 속함
* **Data Access Layer**
  * ORM (Mybatis, Hibernate)를 주로 사용하는 계층
  * DAO 인터페이스와 **@Repository 어노테이션**을 사용하여 작성된 DAO 구현 클래스가 이 계층에 속함 
  * Dabase에 data를 CRUD(Create, Read, Update, Drop)하는 계층
* 기타
  * DTO(Data Tranfer Object)
    * 각 계층간 데이터 교환을 위한 객체 (데이터를 주고 받을 포맷)
    * Domain, VO라고도 부름
    * DB에서 데이터를 얻어 Service, Controller 등으로 보낼 때 사용함
    * 로직을 갖지 않고 순수하게 getter, setter 메소드를 가진다.
  * DAO(Data Access Object)
    * DB에 접근하는 객체, DB를 사용해 데이터를 조작하는 기능을 하는 객체 (MyBatis 사용시에 DAO or Mapper 사용)
    * Repository라고도 부름(JPA 사용시 Repository 사용)
    * Service 계층과 DB를 연결하는 고리 역할을 한다.
  * Entity 클래스
    - Domain 이라고도 부름 (JPA 사용할 때 사용)
    - 실제 DB 테이블과 매칭될 클래스
    - Entity 클래스 또는 가장 Core한 클래스라고 부름
    - Domain 로직만을 가지고 있어야하며 Presentation Logic을 가지고 있어서는 안된다.

---

### AOP

> **관점 지향 프로그래밍**이라고 불린다. 관점 지향은 쉽게 말해 **어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 각각 모듈화하겠다는 것**

* 정의

  * 프로그램의 크기가 엄청나게 커지면서 이러한 모듈 안에서마저 중복되는 코드가 생기게 되는 문제
  * 이를 횡단 관심사(Crosscutting-Concerns)라고 함. 트랜잭션, 로깅, 성능 분석 등
  * 이러한 횡단 관심사들은 여러 모듈들을 말 그래도 횡단하면서 존재

* Spring AOP는 프록시 패턴이라는 디자인 패턴을 사용해서 AOP 효과를 낸다.
* 프록시 패턴을 사용하면 어떤 기능을 추가하려 할때 기존 코드를 변경하지 않고 기능을 추가할수 있다.

---



  

  



