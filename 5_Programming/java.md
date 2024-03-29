# Java

<br>

### 컴파일 순서

1. 개발자가 자바 소스코드(.java)를 작성

2. 자바 컴파일러가 자바 소스코드(.java)파일을 읽어 바이트코드(.class)코드로 컴파일. 바이트코드(.class)파일은 아직 컴퓨터가 읽을 수 없는 JVM(자바 가상 머신)이 읽을 수 있는 코드(java - > class)

3. 컴파일된 바이트코드(.class)를 JVM의 클래스로더(Class Loader)에게 전달

4. 클래스 로더는 동적로딩(Dynamic Loading)을 통해 필요한 클래스들을 로딩 및 링크하여 런타임 데이터 영역(Runtime Data Area), 즉 JVM의 메모리에 로드

5. 실행엔진(Execution Engine)은 JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행합니다. 이 때 실행 엔진은 두 가지 방식으로 변경

---

### 추상클래스/인터페이스

> **추상클래스는 IS - A "~이다".**
>
> **인터페이스는 HAS - A "~을 할 수 있는".**

![image](https://user-images.githubusercontent.com/75229881/136740684-a9aa12cb-935a-42c4-9f5c-22e3358ecc98.png)

**인터페이스**

*  **여러 인터페이스를 상속받는 다중 상속을 지원**한다. 

  ```java
  public interface MyInterface extends  X, Y {}
  인터페이스에서 다중 상속을 할 때는 , 로 구분을 해서 나열한다.
  ```
  



---

### Spring

<br>

**웹 계층**

![image](https://user-images.githubusercontent.com/75229881/169479621-a26f2cac-f21c-41cb-aae1-f87237ae7779.png)

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

<br>

![image](https://user-images.githubusercontent.com/75229881/169478517-3fd136d3-ca6b-487a-9381-6fa131d0913c.png)

* 요청
  * **Request -> DispatcherServlet -> HandlerMapping -> Controller -> Service -> DAO -> DB** 
* 응답
  * **-> DAO -> Service -> Controller -> DispatcherServlet -> ViewResolver -> View -> Response**



---

### MVC 모델

<img src = "https://user-images.githubusercontent.com/75229881/163994778-fe8b6e38-b3df-40c7-bc23-2ed105e710a4.png" width="65%">

**모델**

* 데이터베이스, 상수, 초기화값, 변수 등

1. 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 한다.
   * 화면안의 네모박스에 글자가 표현된다면, 네모박스의 화면 위치 정보, 네모박스의 크기정보, 글자내용, 글자의 위치, 글자의 포맷 정보 등을 가지고 있어야 한다
2. 뷰나 컨트롤러에 대해서 어떤 정보도 알지 말아야 한다
   * 데이터 변경이 일어났을 때 모델에서 화면 UI를 직접 조정해서 수정할 수 있도록 뷰를 참조하는 내부 속성값을 가지면 안 된다
3. 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야만 한다.
   * 모델의 속성 중 텍스트 정보가 변경이 된다면, 이벤트를 발생시켜 누군가에게 전달해야 하며, 누군가 모델을 변경하도록 요청하는 이벤트를 보냈을 때 이를 수신할 수 있는 처리 방법을 구현해야한다.

**뷰**

* input 텍스트, 체크박스 항목 등과 같은 사용자 인터페이스 요소
* 다시 말해 데이터 및 객체의 입력, 그리고 보여주는 출력을 담당

1. 모델이 가지고 있는 정보를 따로 저장해서는 안된다
   * 단순히 네모 박스를 그리라는 명령을 받으면, 화면에 표시하기만 하고 그 화면을 그릴 때 필요한 정보들은 저장하지 않아야 한다.
2. 모델이나 컨트롤러와 같이 다른 구성요소들을 몰라야 된다
   * 뷰는 데이터를 받으면 화면에 표시해주는 역할만
3. 변경이 일어나면 변경통지에 대한 처리방법을 구현해야만 한다
   * 뷰에서는 화면에서 사용자가 화면에 표시된 내용을 변경하게 되면 이를 모델에게 전달해서 모델을 변경해야 할 것이다.

**컨트롤러**

1. 모델이나 뷰에 대해서 알고 있어야 한다
2. 모델이나 뷰의 변경을 모니터링 해야 한다

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

### JUnit

- setUp() : 테스트 대상 클래스의 실행 전에 가장 먼저 setUP()을 실행한다.
  - ex) DB 및 서버 네트워크 환경 연결 시 활용
- tearDown() : 가장 마지막에 수행되며 setUp()의 반대 개념으로 생각하면 된다.
  - ex) DB 및 서버 네트워크 환경 연결 종료 시 활용
- 각 테스트 코드 실행 시 setUp , tearDown 반복 실행한다.

---

### String

* 자바 문자열은 **불변(immutable)**
* 문자열에 연산을 가하면 현재 문자열을 변경되지 않고 변경된 새 문자열이 만들어져서 반환

```java
public class HelloWorld {
    public static void main(String args[]){
        String s0 = "Hello PL.";
        String s1 = "Hello ";
        String s2 = "PL.";
        String s3 = new String("Hello ");
        String s4 = s1 + s2; // 새로운 String Object 생성
        String s5 = "Hello " + "PL.";

        if(s1 == s3) System.out.println("s1 == s3");	// False, s3은 new string
        if(s0 == s4) System.out.println("s0 == s4");	// False, s4는 new string
        if(s0 == s5) System.out.println("s0 == s5");	// True
        if(s1.equals(s3)) System.out.println("s1 == s3");	// True
        if(s0.equals(s4)) System.out.println("s0 == s4");	// True
    }
}

//result
s0 == s5
s1 == s3
s0 == s4

```

---

### 예외처리

**try, throw, catch, finally**

```java
public class Mathematics {
  public static void main(String[] args) {
       int num1, num2;
       int [] intArrayList = {0, 1, 2};
       
       num1 = 12;
       num2 = 0;
       
       try {
            //System.out.println(num1/num2);
            System.out.println(intArrayList[3]);
       } catch (ArithmeticException e) {
            System.out.println("0으로는 값을 나눌 수가 없습니다.");
       } catch (ArrayIndexOutOfBoundsException e) {
       	    System.out.println("배열의 범위를 넘어섰습니다.");
       } finally {
       	    System.out.println("예외 관계없이 실행됨");
       }
  }
}
```

 <br>

**throws**

* **자신을 호출하는 메소드에 예외처리의 책임을 넘긴다**

```java
	public static void main(String args[]){
        try {
            System.out.println("문장 A");
            foo();
            System.out.println("문장 B");
        }
        catch (Exception e){
            System.out.println("문장 C");
        }
        System.out.println("문장 D");
    }

    public static void foo() throws Exception{
        try{
            System.out.println("문장 E");
            throw new Exception();
        }
        catch (Exception e){
            System.out.println("문장 F");
            throw e;
        }
        finally {
            System.out.println("문장 G");
        }
    }

//result
문장 A
문장 E
문장 F
문장 G
문장 C
문장 D
```

---

