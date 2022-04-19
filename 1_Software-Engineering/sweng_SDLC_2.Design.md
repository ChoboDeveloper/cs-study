# 소프트웨어공학/SDLC/2.모델링

<br>

### UML 다이어그램

![image](https://user-images.githubusercontent.com/75229881/163380416-ed05a942-8737-450d-a364-ccf7cef6d949.png)

**클래스 다이어그램**

* 시스템을 구성하는 클래스들 사이의 관계를 표현한다.

* 클래스

  <img src = "https://user-images.githubusercontent.com/75229881/163380610-6fd45f3e-2c57-4b66-9272-fe3c3bea240c.png" width="70%">

  <img src = "https://user-images.githubusercontent.com/75229881/163380824-fed40751-f76e-4f44-be36-43d16bba22ed.png" width="40%">

* 관계

  ![img](https://gmlwjd9405.github.io/images/class-diagram/association.png)

  <img src = "https://user-images.githubusercontent.com/75229881/163381077-3128013d-2752-4e6b-8151-903377160834.png" width="60%">
  
* 연관(Association)

  * **Association은 다른 객체의 참조를 가지는 필드**를 의미
  * 즉 멤버변수로 선언하여 **지속적으로 관계**를 맺는 것을 의미한다.

* 의존

  * Dependency는 클래스간의 참조가 일어나는 것
  * Dependency 참조는 메서드 내에서 대상 클래스의 객체를 생성하거나 사용, 리턴받아 사용하는 것
  * 즉, **멤버변수로 사용하지 않고 메소드의 파라미터, 지역변수**로 활용하는 것이며 잠시 관계를 맺는 것이다.

* 일반화(Generalization)

  * 상속을 의미

* 실체화(Realization)

  * Realization은 interface에 있는 spec을 오버라이딩하여 실제로 구현하는 것

* 집합

---