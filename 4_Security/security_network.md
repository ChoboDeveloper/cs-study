# 네트워크 보안

<br>

### 프록시 서버

* 서버와 클라이언트 사이의 통신에서 중계하는 역할을 한다
* Why?
  * 캐시 데이터를 사용하기 위해
    * 전송시간과 외부트래픽을 줄일 수 있음
  * 보안상의 이유로
    * ip를 숨길 수 있음
  * HTTP 트래픽 모니터링 및 수정

**HTTP 프록시를 이용한 SSL**

* CONNECT 메소드를 활용하여 클라이언트는 원하는 목적지와의 TCP 연결을 HTTP 프록시 서버에 요청
* 브라우저와 웹 서버 사이에 SSL/TLS 핸드셰이크가 수행되며, 프록시 서버는 TCP를 통해 이들을 중계한다.

---

### 방화벽 역사

##### 1세대 방화벽: 패킷 필터

* 정해진 규칙에 맞게 패킷 자체만을 가지고 흐름을 제어하는 비교적 단순한 방법. **IP와 PORT를 통해 패킷을 필터링**했고, 세션은 관리하지 않은 특징이 있다. 따라서 우회적인 공격이나 TCP Header의 DATA를 체크하지 않아 바이러스 등에 취약하다.
* **Layer 4 까지 필터링**
* 이 방식은 모든 패킷을 검사하기에 처리 속도가 매우 느렸으며 FTP 등과 같은 부가 세션을 만드는 프로토콜 지원을 위해서는 포트 전체를 열어야 하는 단점이 존재
* 블랙리스트와 화이트리스트를 가지고 관리하므로 관리자가 직접 리스트를 생성해야 함

**2세대 방화벽 : 상태검사(Stateful Inspection)**

* 패킷 필터의 단점을 해결하기 위해서 고안된 것이 패킷 단위의 검사가 아닌 **세션 단위의 Inspection**
* 패킷의 경로와 거부 내역 등을 모두 기록하는데 이때 모든 상태 채널을 목록에 저장한 후 분석하여 허가여부를 결정하는 방식
* 2세대 방화벽은 화이트리스트를 자동적으로 처리하는 것이 특징

**3세대 방화벽 : 어플리케이션 방화벽**

* I초창기에 네트워크를 기반으로 하던 공격 패턴이 점차 발달하여 일상적인 트래픽과 같은 특성을 가지면서 시스템을 공격하는 형태로 발전하게 되었다. 패킷 필터 기반의 방화벽으로는 이러한 공격을 방어하기 어려워지면서 패킷의 내용을 검사하고 더 나아가서는 애플리케이션에 어떠한 영향을 미칠지를 분석하는 방화벽이 출현하기 시작한다.
* **Layer 7 까지 필터링**
* IPS, WAF, UTM
* UTM(통합위협관리)
  * 기존에 독립적으로 수행하여 왔던 각 솔루션들의 보안 기능들을 통합하여 하나의 장비로 통합보안관리가 가능하도록 지원하는 제품이며, 하나의 보안 어플라이언스에 여러 가지 보안 기능을 통합한 보안 플랫폼으로써 IPS, VPN, 안티 스파이웨어, 안티 바이러스 등의 기능을 하나의 장비 안에서 해결

---

### 방화벽 방식

**패킷 필터링**

* 1세대 방화벽
* 네트워크/전송계층에서 동작하며 속도가 빠르다.
* 패킷의 조작이 가능하여 보안 취약성이 있음
* 접속 제어 규칙의 검증에 따라 방화벽에 부하를 많이 줄 수 있음

**어플리케이션 게이트웨이 방식(응용 레벨 게이트웨이)**

* 7계층 전 구간에서 동작
* 서비스마다 별도의 프록시가 구동되어 서버와 클라이언트 사이에서 관리를 하게되고 반드시 프록시를 거쳐가야 함
* 패킷 필터링 보다 보안성이 우수하지만 처리속도가 떨어진다는 단점이 있다.
* 클라이언트-서버 사이의 **베스천 호스트에 여러 개의 프록시**가 위치

**서킷 게이트웨이 방식(회선 레벨 게이트웨이)**

* 5~7 계층에서 동작
* 통합된 하나의 프록시가 관리
* 내부의 IP를 숨길수 있어서 보안성이 좋지만, 각 클라이언트들은  서킷 게이트웨이를 인식할 수 있는  인식할수 있는 클라이언트 프로그램이 필요(ex. SOCKS)
* 클라이언트-서버 사이의 베스천 호스트에 한 개의 프록시가 위치

```
* 종단간 TCP 연결을 허용하지 않는다.
* 프록시는 내/외부 각각 하나의 TCP를 연결을 설정한다.
```

**하이브리드 방식**

* 하이브리드 방식은 패킷 필터링과 어플리케이션 게이트웨이 방식을 혼합한 것
* 관리와 설치가 복잡하다.

**상태 검사 방식**

* 2세대 방화벽이다
* 패킷 필터의 단점을 해결하기 위해서 고안된 것이 패킷 단위의 검사가 아닌 세션 단위의 검사를 하는 스테이트풀 검사이다.

* 2-3 계층에서 동작
* 패킷들을 상태정보 테이블에 일정시간 저장하여 빠른속도로 처리하고 패킷변조를 막을 수 있다.

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

* 설치위치에 따른 분류
  * **호스트 기반**
    * 각 호스트에 IDS모듈이 설치되어 시스템의 오남용 및 불법적 접근을 탐지하고 이를 관리자에게 통보
    * OS에 종속적이므로 이기종 네트워크환경에서 운영/관리 편의성 저하 및 시스템 부하 가중
  * **네트워크 기반**
    * 일반적인 IDS를 의미하는 것으로, 네트워크의 물리적 혹은 논리적 경계지점에서 동작
* 탐지기법에 따른 분류
  * **오용탐지**
    * 악성패킷 등을 분석한 **침입 패턴**(Rule Set)을 저장하여 패턴과 동일하면 탐지
    
    * 오탐율(False Positive)이 낮지만, 미탐율(False Negative)가 높음
    
    * 제로데이 공격(Zero-day Attack)을 탐지할 수 없으며, 오용탐지를 **시그니처(Signature) 기반 혹은 지식(Knowledge) 기반**의 탐지 방법이라고 부른다.
    
  * **이상탐지**
    * **정상 패턴**을 저장하고 이와 다르면 탐지하는 방식
    * 오탐율이 높지만, 미탐율이 낮음
    * 제로데이 공격에 대응

---

### IDS 판정

**Confusion Matrix**

|           | Positive             | Negative             |
| --------- | -------------------- | -------------------- |
| **True**  | True Positive        | False Negative(오탐) |
| **False** | False Positive(미탐) | True Negative        |

---

### IPS

**Snort**

* 패킷 스니퍼
  * 패킷탐지
* 패킷 로거
  * 패킷의 로그를 기록
* 네트워크 침입 탐지

---

### NAC 구성방식

**802.1x 방식**

**VLAN 방식**

* 물리적 배치와 상관없이 논리적으로 LAN을 구성할 수 있는 기술

* VLAN이 없으면 스위치에 연결대수가 많아질수록 브로드캐스팅에 의한 부하가 심화됌

* 종류

  * **Port 기반**
  * MAC 기반
  * Network 기반
  * 프로토콜 기반

* 관련기술
  * Port Mirroring
    * VLAN의 모든 패킷들을 다른 모니터링 포트로 복제하여 패킷을 분석
    * 스위치 네트워크의 **성능, 트래픽 분석**을 위하여 사용
    
  * Trunking

    ![image](https://user-images.githubusercontent.com/75229881/168592441-c14c4a79-bcb1-43ba-bde9-abe16d51e42e.png)

    * VLAN 이 N개 일때 스위치간 링크는 N개, **Trunking**은 VLAN 이 N개 여도 하나의 통합 링크를 통해서 패킷을 보내는 방식
    * 하나의 통합 링크를 통해 보내므로 각 패킷이 포함된 VLAN 정보를 알수 없음. 따라서 패킷에 자신의 VLAN 정보를 넣어 보내는 방식을 사용(**Tagging**)
    * 즉, 다시말해 스위치 하나가 아닌 서로 다른 스위치의 장비를 같은 VLAN 으로 묶고 싶을 때 VLAN 정보를 스위치간에 공유해야되는데 이 VLAN 정보를 공유하는 것이 Trunking
    * Tagging 이란 과정을 이용해 교환하는 규칙이 **VTP(VLAN Trunking Protocol)**
    * Trunking 이 지원되지 않는다면 스위치에 만들어진 VLAN의 개수만큼 스위치끼리 링크가 필요할 것

  * Pruning
    * 필요 없는 브로드캐스트 트래픽이 Trunk 포트를 통하여 전송되는 것을 차단

**ARP 방식**

**에이전트 방식**

**DHCP 방식**

* MAC 주소를 확인하여 허가된 IP 대역 / 비허가된 IP 대역으로 구분한다.

---

### 패킷 제어방식

**미러링**

* 미러링 방식은 **TAP 장비**나 네트워크 장비의 미러링 포트 기능을 설정하여 네트워크 트래픽의 복사본을 **모니터링 하는 방식**이다. (스니핑 방식)
* TAP장비란 Network상의 한 구간에 이동하는 Packet을 복사하여 Monitor 장비로 보내주는 역할
* **사후감사**에 중점을 둔 방식

**인라인**

* 인라인방식은 방화벽과 동일하게 위치시켜 모든 트래픽을 IDS를 거치도록 하는 방식
* **사전감사**에 중점을 둔 방식

**프록시**

> Proxy를 만들어서 **클라이언트에겐 내가 서버인 것처럼 나한테 접속하게 하고 서버에겐 내가 클라이언트인 것처럼 서버에 접속**

*  네트워크 장비 없이 순수하게 **프로그램만으로 구동**되는 방식
* 위에서 HTTPs / SSL / SSH 등은 데이터를 암호화해서 전송하게 되어 있다. 그래서, 미러링 / Inline으로 패킷을 받아도 해당 내용을 확인할 수 없습니다. Key가 있어야 하는데 이것은 고유 Key여서 제3자가 암호를 풀 수가 없다. 그렇기 때문에 Proxy를 만들어 클라이언트는 내가 서버인 줄 알고 나한테 접속하여 서로 key를 교환하고 나는 내가 클라이언트인 것처럼 서버에 접속하여 서로 key 교환을 하여 패킷을 확인할 수 있다.

---

