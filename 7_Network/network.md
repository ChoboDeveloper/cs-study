# 네트워크

<br>

### OSI 7 Layer

* 응용
  * 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다
  * 응용 프로세스의 실행에 필요한 HTTP, FTP 등의 프로토콜을 제공한다
  
* 표현
  * 응용 계층으로부터 전송받거나 응용 계층으로 전달해야 할 데이터의 인코딩과 디코딩이 이 계층에서 이루어진다. 그리고 표현 계층은 데이터를 안전하게 사용하기 위해서 암호화와 복호화를 하는데 이 작업도 표현 계층에서 이루어진다. 
  * 예를 들면 유니코드(UTF-8)로 인코딩 되어있는 문서를 ASCII로 인코딩 된 문서로 변환하려 할 때 이 계층에서 변환이 이루어진다.
  
* 세션
  * 세션을 통해 통신장치간의 연결을 관리한다. 즉 연결상태 혹은 동기화등을 통해 연결정보에 대한 관리 역할을 한다.
  
* 전송
  * 통신을 활성화하기 위한 계층이다. 보통 TCP프로토콜을 이용하며, 포트를 열어서 응용프로그램들이 전송을 할 수 있게 한다.
  * 즉 포트가 열리면 패킷이 생성되고 전송된다. 또한, 이 과정에서 흐름제어, 오류제어, 혼잡제어 등 신뢰성 있는 통신을 제공한다.
  * 전송단위는 세그먼트
  
* 네트워크
  
  > IP, ICMP, OSPF, DDP(Datagram Delivery)
  
  * 라우팅 과정에서 경로설정 및 패킷 스위칭 기능을 한다.
  * 전송단위는 **패킷**
  
* 데이터링크

  > PPP, FDDI, HDLS, ATM, SLIP(Serial Line)

  * **물리 계층을 통해 송수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달**을 수행할 수 있도록 도와주는 역할을 한다. 따라서 통신에서의 오류도 찾아주고 재전송도 하는 기능을 가지고 있는 것이다.
  * 데이터링크 계층에서는 MAC 주소를 가지고 통신하게 된다.
  * 이 계층에서 전송되는 단위를 **프레임**이라고 하고, 대표적인 장비로는 **브리지, 스위치** 등이 있다.

* 물리
  * 물리계층에서는 주로 전기적, 기계적, 기능적인 특성을 이용해서 통신 케이블로 데이터를 전송하게 된다.
  * 전송케이블, 리피터, 허브등이 이에 속한다.

---

### TCP

**흐름제어**

* 송신측과 수신측 사이의 데이터 처리 속도 차이(흐름)을 해결하기 위한 기법
* Stop and Wait
  * 매 패킷에 대한 응답
* Sliding Window
  * 수신측에서 설정한 윈도우 크기만큼 송신측에서 확인 응답 없이 세그먼트를 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하는 기법이다. 
  * **Window**는 송신, 수신 스테이션 양쪽에서 만들어진 버퍼의 크기 

**오류제어**

* Stop and Wait
* Go Bank-N ARQ
* Selective ARQ

**혼잡제어**

---

### UDP

* 재전송 없음, **체크섬** 있음

| TCP                                                          | UDP                                                          |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| Connection-oriented protocol (연결지향형 프로토콜)           | Connection-less protocol (비 연결지향형 프로토콜)            |
| Connection by **byte** stream (바이트 스트림을 통한 연결)    | Connection by **message** stream (메세지 스트림을 통한 연결) |
| Congestion / Flow control (혼잡제어, 흐름제어)               | NO Congestion / Flow control (혼잡제어와 흐름제어 지원 X)    |
| Ordered, Lower speed (순서 보장, 상대적으로 느림)            | Not ordered, Higer speed (순서 보장되지 않음, 상대적으로 빠름) |
| Reliable data transmission (신뢰성 있는 데이터 전송 - 안정적) | Unreliable data transmission (데이터 전송 보장 X)            |
| TCP packet : Segment (세그먼트 TCP 패킷)                     | UDP packet : Datagram (데이터그램 UDP 패킷)                  |
| HTTP, Email, File transfer 에서 사용                         | **DNS**, Broadcasting (도메인, 실시간 동영상 서비스에서 사용) |

---

### IPv6

* 128비트 주소를 사용(16 옥텟)
  * 따라서 IP주소를 절약하기 위해 사용되는 NAT와 같은 주소변환 기술도 불필요
* 고정길이 헤더
  * 패킷 단편화(fragmentation) 관련 필드가 삭제
    * 라우터 부하를 줄이기 위해
  * 체크섬 (checksum) 필드 삭제
    * 데이터 신뢰성이 높아졌기 때문
    * 오류제어는 데이터링크 계층에서 CRC를 통해 미리 체크함 혹은 전송계층에서
* 트래픽을 효율적으로 관리
  * FlowLabel 필드 활용
* 보안기능
  * 확장헤더를 활용한 종단간 암호화 제공(IPsec)
* 자동 주소설정
  * 로컬 IPv6주소를 LAN상의 MAC주소와 라우터가 제공하는 네트워크 프리픽스(prefix)에 결합하여 IP주소를 자동 생성
* Anycast, Unicast, Multicast

---

### 라우팅 프로토콜

|          라우팅 방식           |          설명          |
| :----------------------------: | :--------------------: |
| Interior Gateway Protocol(IGP) | RIP, IGRP, OSPF, IS-IS |
| Exterior Gateway Protocol(EGP) |          BGP           |

* IGP는 네트워크 내부에서 데이터를 보내는 경우
* EGP는 게이트웨이의 외부를 거쳐서 데이터를 보내야 할 경우

|                 라우팅 방식                 |                             설명                             |
| :-----------------------------------------: | :----------------------------------------------------------: |
| Distance Vector Routing Algorithm(거리벡터) | RIP, IGRP<br>근처 노드와의 정보교환을 통한 라우팅 테이블 갱신 |
|   Link State Routing Algorithm(링크상태)    | OSPF, IS-IS<br>모든 노드의 링크상태와 비용을 라우팅 테이블로 구성 |
|            Path Vector(경로벡터)            |         BGP<br>거리와 관계없이 목적지의 경로를 탐색          |

**RIP**

* 특징
  * 거리벡터 알고리즘에 기초하여 개발된 라우팅 프로토콜
  * 최대 15 홉
  * 벨만포드 알고리즘 활용
  * Distance-Vector

* **Route poisoning :** RIP은 특정 network가 down 되면 즉시 해당 network(down 된 network)의 metric 값을 16으로 설정해 인접 router에게 flash update를 전송함으로 해당 network가 down되었다는 것을 알린다.
* **Poison reverse :** route poisoning을 받은 router는 자신의 RIP database를 보고 해당 network에 대한 대체 경로가 없을 시 route poisoning을 보낸 인접 router에게 해당 network의 metric 값을 16으로 설정해 역으로 보내서 대체 경로가 없다는 것을 알려준다. (대체 경로가 있다면 poison reverse를 보내지 않는다.)

**OSPF**

* 대규모 네트워크에 적합
* RIP에 비해 Hop count 제한이 없고 Convergence(수렴) 시간이 빠름
* 라우팅 정보를 주기적이 아닌 변화가 있을 때에만 갱신함
* 동일한 네트워크 주소에서 VLSM (Variable Length Subnet Mask)를 사용하여 한정된 주소를 효율적으로 이용할 수 있음
* Link-State
  * 각각의 라우터는 각 인터페이스의 정보를 포함한 접속정보를 생성하고 유지하여 한 AS 내에 있는 모든 라우터에게 접속 정보를 전달한다.
  * 라우터들은 각각 고유 Database를 작성하고 보유하고 있다.
  * 모든 라우터들은 최단경로 알고리즘(다익스트라)으로 동작하고 접속정보를 기초로 하여 최단 경로를 설정한다.

**BGP**

* Path-Vector(경로벡터)
  * 거리 상관 x, 경로에 기반한 라우팅, 스패닝 트리


---

### 윈도우 네트워크 명령어

* netstat
  * 네트워크 연결, 라우팅 테이블, 네트워크 장치의 통계정보 등 네트워크에 관련된 여러 가지 정보를 확인 할 수 있다.
* ping
  * 목적지의 네트워크 상태 및 RTT 정보(왕복시간) 제공

* tracert
  * tracert는 출발지부터 목적지까지의 경로 정보를 출력
  * ICMP, TTL, UDP를 활용한다
  * TTL을 1씩 키워서 전송하고 ICMP time exceed 메시지를 받아서 경로를 역추적
* route
  * 라우팅 테이블의 정보 확인
  * 네트워크 목적지, 네트워크 마스크, 게이트웨이, 인터페이스, 메트릭으로 구성
* nslookup
  * 도메인 정보 조회, IP 주소 출력

---

### IP Class

**Class A**

* 대규모 네트워크 환경
* 0.0.0.0 ~ 127.255.255.255

**Class B**

* 중규모
* 10.0.0.0 ~ 191.255.255.255 

**Class C**

* 110.0.0.0 ~ 223.255.255.255

**Class D**

* 멀티캐스트용

**Class E**

 * 실험용

**참고**

* 사설망
  * 10.0.0.0 - 10.255.255.255 // (10.0.0.0/8)
  *  172.16.0.0 - 172.31.255.255 // (172.16.0.0/12)
  * 192.168.0.0 - 192.168.255.255 // (192.168.0.0/16)

---

### 서브넷마스크

> **네트워크 영역을 늘리고 호스트 영역을 줄일 수 있음**

* IP주소와 서브넷마스크를 논리 AND 연산하면 서브넷네트워크를 구할 수 있다.
* 예시로 155.16.32.* , 155.16.33.* 은 원래 동일 네트워크지만 서브넷을 통해 다른 네트워크로 구성할 수 있다.

**참고**

* 일반적으로(C class) 256개의 호스트 중 **0은 네트워크, 255는 브로드캐스트, 1개는 게이트웨이**로 총 253개의 주소 사용가능하다

**예제문항**

* 192.168.51.110/20
  * 서브넷마스크 : 255.255.240.0
  * 네트워크 수 : 256/16 = 16개
  * 네트워크 주소 : 192.168.48.0
  * 기본 게이트웨이 주소 : 192.168.48.1
  * 브로드캐스트 주소 : 192.168.63.255 (Host bit를 모두 1로 채움)

**FLSM**

<img src = "https://user-images.githubusercontent.com/75229881/126755813-183540b6-0bbf-4f44-9b4a-b81315f286d0.png" width="40%">

* **Fixed Length Subnet Mask**

* 서브넷의 길이를 고정적으로 사용하는 것

**VLSM**

<img src = "https://user-images.githubusercontent.com/75229881/126755898-0b1ee233-dc4d-4463-979c-7eb02a17b449.png" width="60%">

* **Variable - Length Subnet Mask**

* 서브넷의 길이를 가변적으로 사용하는 것

---

### CDMA 복합신호

* 비트가 '0' 이면 -1, 1이면 +1의 신호를 가진다

<img src = "https://user-images.githubusercontent.com/75229881/127096369-ccddb361-7729-40ed-8e16-cdb6645e9c6b.png" width="80%">

* 각 노드의 칩 순열에 따라 곱 연산을 실행하고 이를 합산하여 공통 채널의 디지털 신호를 구할 수 있다


<img src = "https://user-images.githubusercontent.com/75229881/127096435-b17fb9b6-2e58-4984-a90b-1384a35b97ab.png" width="80%">

<img src ="https://user-images.githubusercontent.com/75229881/127096552-153fb711-d1d1-49ee-8789-325ebdecf1de.png " width="80%">

* 복호화 과정에서 공통 채널의 디지털 신호와 해당 노드의 칩 순열의 곱 연산을 통해 구한 값을 모두 더하여 값의 합을 노드수로 나눠 비트를 검출할 수 있다.

<img src ="https://user-images.githubusercontent.com/75229881/127096710-ea070f47-2b79-4883-af30-b07280f5cbc7.png " width="80%">



---

### 국제표준

**IMT**

* IMT-2000 : 3G 네트워크
* IMT-Advanced : 4G, LTE 네트워크
* IMT-2020 : 5G 네트워크

---

### IP Fragmentation

- 패킷을 전송하고자 하는데 패킷의 크기가 MTU(Maximum Transmission Unit)을 초과하면 한번에 전송할 수 없다.
- 패킷을 MTU 이하의 조각으로 분할하는 것을 단편화(Fragmentation), 분할된 조각을 단편(Fragment)이라고 한다.

**단편화 예시**

- 4000바이트의 패킷을 전송하려고 하는데 MTU가 1500이다.
- 패킷은 아래와 같이 분할된다.

| 순서 | 페이로드 | 헤더 | More Flag | offset |
| :--: | :------: | :--: | :-------: | :----: |
|  1   |   1480   |  20  |     1     |   0    |
|  2   |   1480   |  20  |     1     |  185   |
|  3   |   1020   |  20  |     0     |  370   |



---

### SDN

* 네트워킹 리소스를 가상화된 시스템으로 추상화하는 IT Infra에 대한 하나의 접근 방식
* 개방형 API(오픈플로우)를 통해 네트워크의 트래픽 전달 동작을 소프트웨어 기반 컨트롤러에서 제어/관리하는 기술

<br>

**OpneFlow**

* SDN에서 컨트롤러와 네트워크 장비간의 **개방형 인터페이스**를 위한 규격으로 사용되는 기술
* SDN은 소프트웨어로 전환하는 것이 아니라 소프트웨어로 하드웨어를 통제하는 개념이다. 오픈플로우 스위치는 하나 이상의 플로우 테이블과 그룹 테이블을 가질 수 있다.
* 구성요소
  1. 플로우 테이블(flow table)
     * 플로우 테이블은 리스트 형식으로 다수의 entry를 갖는다. 이러한 entry를 flow entry라고 하는데 flow entry는 3가지의 메인 컴포넌트들을 가지고 있다.
     * match fields : 패킷의 매칭되는 field. ingress port와 packet header들 그리고 옵션적으로 이전 테이블에서 정의된 metadata등이 있다.
     * counters : 매칭된 패킷의 통계적인 정보를 위해 패킷이 매칭될때 마다 여러가지의 counter를 사용하여 통계정보에 활용한다.
     * instructions : 액션 set을 수정하거나 파이프라인 프로세싱을 진행한다.
  2. 그룹 테이블(group table)
     * Group Table은 flow table의 확장판이다. 하지만 비슷해 보이지만서도 다른부분이 많다. 결론적으로는 한번에 여러 action을 수행하기 위한 테이블이다.
     * group identifier : Group entry를 구분할 수 있도록 해주는 32bit unsigned integer
     * group type : group entry에 정의된 bucket들을 일부만 수행할 것인지(select) 전부 수행할 것인지(all)에 대한 규칙이 명시되어있다.
     * counter : flow table의 counter와 마찬가지로 통계를 위해 사용된다.
     * action buckets : action bucket은 말그대로 action'들'을 가지고 있고 그 action들을 가지고 있는 action bucket'들'을 하나의 group entry가 가지고 있다.
  3. 네트워크 기능 가상화(network function virtualization)
     * 하드웨어 기반의 네트워크 장비를 소프트웨어 기반의 가상화 기기로 전환하는 기술이다.
  4. 파이프라인 처리(pipelining)
     * 오픈플로우 스위치에서 매칭 포워딩 패킷 수정을 제공하는 연결된 테이블의 집합을 의미

**NFV(Nerwork Function Virtualization)**

* NFV란 기존의 네트워크 하드웨어 장비를 소프트웨어 형태로 가상화하는 개념이다.
* 즉, 라우터(Router), 방화벽(Firewall), 로드밸런서(Load Balancer), IDS, IPS, DNS, 캐싱 등의 물리적인 네트워크 기능을 여러 사용자 또는 필요한(+저렴한) 리소스(서버, 스토리지 등)에서 사용할 수 있는 것이다.

<br>

> **SDN**은 네트워크의 제어 기능과 전달 기능을 소프트웨어로 분리하여 추상화시키는 것이다.
>
> 좀더 엄밀히 말하면 Control Plain을 소프트웨어화 시키는 것이다.
>
> OSI 7Layer 기준으로 SDN은 2-3 Layer를 담당하며, 스위치, 라우터, 무선 access 포인트 같은 네트워크 인프라를 최적화한다.
>
> ---
>
> **NFV**는 네트워크 Appliance 기능을 가상화하여 하드웨어와 소프트웨어로 분리하는 것이다.
>
> 네트워크 기능 가상화에 초점이 맞춰져 있으며, 이는 Data Plain을 가상화한다는 의미이다.
>
> OSI 7Layer 기준으로 NFV는 4-7 Layer를 포함하며, Edge 인증, 로드밸런서, 방화벽, WAN 컨트롤러 등의 네트워크 기능의 배포를 최적화한다.

---

### 이동 IP 프로토콜

> 이동하는 사용자가 서비스 중단 없이 인터넷에 접속할 수 있는 이동 환경 서비스를 수용하는 문제

* IP 주소가 이동망 환경에서 들어오게 되면 IP 주소를 추적할 수 있는 기능이 필요하게 된다. 그래서 **에이전트**를 사용하게 된다.
* 두 종류의 주소를 사용하게 되는데 **Home Address는 이동 호스트를 위한 고정 주소**를 나타낸다. 
  * 홈 에이전트는 이동 호스트를 위한 고정 위치(고정 주소)에서 포린 에이전트로의 연결을 처리한다.
  * 홈 에이전트로 라우팅 된 패킷을 이동 호스트에 전달하려면 터널링을 통해 전달해야 한다.
  * 터널링을 통해 송신호스트와 수신호스트 사이에 추가적인 IP 프로토콜을 사용하여 패킷을 중개해야 한다.
* **COA(Care of Address)**는 **이동 호스트를 위한 가변 주소**로 일시적으로 할당된다. COA는 이동 호스트가 위치를 변경할 때, 새로 이동한 지역에서 일시적으로 할당된 IP 주소이다. 

---

### HTTP 상태코드

**4XX: Client error**

- 400 Bad Request
  - 클라이언트가 올바르지 못한 요청을 보내고 있음을 의미
- 401 Unauthorized
  - 요청을 위해서는 권한 인증등을 요구함을 의미
- **403 Forbidden**
  - 요청이 서버에 의해 거부 되었음을 의미, 서버는 거부 이유를 포함하여 응답할 수 있지만, 보통은 거부 이유를 숨기고 싶을 때 사용된다.
- **404 Not Found**
  - 요청한 URL을 찾을 수 없음을 의미
- 405 Method Not Allowed
  - 요청한 URL이 Method를 지원하지 않음을 의미(ex] POST요청에 대한 응답을 하는 URL에 GET으로 요청)
- 406 Not Acceptable
  - 클라이언트 요청에 대해 적절한 컨텐츠가 없음을 의미
- 407 Proxy Authentication Required
  - 401과 동일하나, 프락시(우회경로)를 통하여 인증 할 것을 요구함을 의미
- 408 Request Timeout
  - 오래 사용하지 않아서 서버가 연결을 끊음
- 409 Conflict
  - 클라이언트 요청에 대해 서버에서 충돌 요소가 발생 할수 있음을 의미
- 410 Gone
  - 요청한 URL이 더 이상 사용되지 않고 사라졌음을 의미
- 413 Payload Too Large
  - Request의 Payload 너무 커서 서버가 처리 할 수 없음을 의미
- 414 URL Too Long
  - Request URL이 너무 길어 처리 할 수 없음을 의미
- 415 Unsupported Media Type
  - 서버가 이해 하지 못하는 유형의 컨텐츠를 요청 하였음을 의미
- 416 Requested Range Not Satisfiable
  - 클라이언트의 요청 내용이 범위가 잘못되었음을 의미
- 429 Too Many Requests
  - 사용자가 지정된 시간에 너무 많은 요청을 보냈습니다

<br>

**5XX: Server error**

* **500 Internal Server Error**
  * 서버에 오류가 발생하여 응답 할 수 없음
* **501 Not Implemented**
  * 클라이언트 요청에 대한 **서버의 응답 수행 기능이 없음**을 의미(ex] 서버가 지원하지 않는 새로운 Method를 사용하여 요청 - GET2, POST2...)
* **502 Bad Gateway**
  * 서버가 게이트웨이로부터 잘못된 응답을 수신했음을 의미합니다. 인터넷상의 서버가 다른 서버로부터 유효하지 않은 응답을 받은 경우 발생
* **503 Service Unavailable**
  * 유지보수를 위해 작동이 중단되거나 과부하가 걸린 서버
* 504 Gateway Timeout

  * 서버에서 다른 서버로 요청을 보냈으나, 응답 지연이 발생하여 처리가 불가함
* 505 HTTP Version Not Supported

  * 서버에서 지원되지 않는 HTTP 버전을 클라이언트가 요청
* 506 Variant Also Negotiates

  * 서버에 내부 구성 오류
* 507 Insufficient Storage

  * 서버 스토리지 부족
* 508 Loop Detected (WebDAV)
* 서버가 요청을 처리하는 동안 무한 루프를 감지
* 510 Not Extended
* 서버가 요청을 이행하려면 요청에 대한 추가 확장이 필요
* 511 Network Authentication Required
  * 클라이언트가 네트워크 액세스를 얻기 위해 인증할 필요가 있음

---
