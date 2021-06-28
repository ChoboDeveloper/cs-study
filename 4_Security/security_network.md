# 네트워크 보안

<br>

### 방화벽 방식

**패킷 필터링**

* 1세대 방화벽
* 네트워크/전송계층에서 동작하며 속도가 빠르다.
* 패킷의 조작이 가능하여 보안 취약성이 있음
* 접속 제어 규칙의 검증에 따라 방화벽에 부하를 많이 줄 수 있음

**어플리케이션 게이트웨이 방식**

* 7계층 전 구간에서 동작
* 서비스마다 별도의 프록시가 구동되어 서버와 클라이언트 사이에서 관리를 하게되고 반드시 프록시를 거쳐가야 함
* 패킷 필터링 보다 보안성이 우수하지만 처리속도가 떨어진다는 단점이 있다.
* 클라이언트-서버 사이의 베스천 호스트에 여러 개의 프록시가 위치

**서킷 게이트웨이 방식**

* 5~7 계층에서 동작
* 통합된 하나의 프록시가 관리
* 내부의 IP를 숨길수 있어서 보안성이 좋지만, 각 클라이언트들은  서킷 게이트웨이를 인식할 수 있는  인식할수 있는 클라이언트 프로그램이 필요
* 클라이언트-서버 사이의 베스천 호스트에 한 개의 프록시가 위치

**상태 추적 방식**

* 2-3 계층에서 동작
* 패킷들을 상태정보 테이블에 일정시간 저장하여 빠른속도로 처리하고 패킷변조를 막을 수 있다.

**하이브리드 방식**

* 하이브리드 방식은 패킷 필터링과 어플리케이션 게이트웨이 방식을 혼합한 것
* 관리와 설치가 복잡하다.

---

### 방화벽 구조

**스크리닝 라우터**

* 라우터가 패킷필터링 규칙을 적용해서 방화벽의 역할을 수행하는 구조
* 세부적인 규칙을 적용하기 어렵고 만약에 접속이 폭주할경우 부하가 걸려 비효율적
* 저렴하게 구축가능

**단일 홈 게이트웨이**

![image](https://user-images.githubusercontent.com/75229881/119295258-58bd1a80-bc91-11eb-83e8-9c89fd11347b.png)

* 베스천 호스트 사용

* 접근제어, 프록시, 인증, 로깅 등 방화벽의 기본 기능을 수행

**이중 홈 게이트웨이**

![image](https://user-images.githubusercontent.com/75229881/119295272-68d4fa00-bc91-11eb-8dc9-05de5be1e84d.png)

* 베스천 호스트 사용

* 외부 네트워크에 대한 네트워크 카드와 내부 네트워크에 대한 네트워크 카드를 구분하여 운영 
* 단일 홈 게이트웨이보다 효율적으로 트래픽 관리 가능

**스크린드 호스트 게이트웨이**

<img src = "https://user-images.githubusercontent.com/75229881/119295411-c1a49280-bc91-11eb-8da4-c941893e01ca.png" width="50%">

* 라우터 + 베스천 호스트 사용

* 스크리닝 라우터와 단일 혹은 듀얼 홈 게이트웨이와 조합해서 사용하는 방식
* 라우터로 패킷 필터링 후 베스천 호스트로 방화벽 임무 수행

**스크린드 서브넷 게이트웨이**

<img src = "https://user-images.githubusercontent.com/75229881/119295371-9fab1000-bc91-11eb-90c4-0c3bcf8b9a57.png" width="50%">

* 라우터 + 베스천 호스트 + 라우터 사용

* 스크린드 서브넷 게이트웨이 방식은 외부와 내부의 가운데에 DMZ(DeMilitarized Zone)를 위치시켜 프록시를 설치하여 완충지대를 구성

---

### 방화벽/IDS/IPS

![image](https://user-images.githubusercontent.com/75229881/119295114-f9f7a100-bc90-11eb-95d1-5a5cc1eb58c2.png)

---

### IDS

**오용탐지**

* 악성패킷 등을 분석한 **침입 패턴**(Rule Set)을 저장하여 패턴과 동일하면 탐지
* 오탐율(False Positive)이 낮지만, 미탐율(False Negative)가 높음
* 제로데이 공격(Zero-day Attack)을 탐지할 수 없으며, 오용탐지를 **시그니처(Signature) 기반 혹은 지식(Knowledge) 기반**의 탐지 방법이라고 부른다.

**이상탐지**

* **정상 패턴**을 저장하고 이와 다르면 탐지하는 방식
* 오탐율이 높지만, 미탐율이 낮음
* 제로데이 공격에 대응

---

### IDS 판정

|                 | 정상 패킷            | 비정상 패킷          |
| --------------- | -------------------- | -------------------- |
| 정상으로 탐지   | True Positive        | False Negative(미탐) |
| 비정상으로 탐지 | False Positive(오탐) | True Negative        |

* True : 맞음, False : 틀림
* Positive : 정상패킷, Negative : 비정상 패킷

---
