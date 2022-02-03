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
  * 라우팅 과정에서 경로설정 및 패킷 스위칭 기능을 한다.
  * 전송단위는 **패킷**
* 데이터링크
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

* 128비트 주소를 사용
  * 따라서 IP주소를 절약하기 위해 사용되는 NAT와 같은 주소변환 기술도 불필요
* 고정길이 헤더
  * 패킷 단편화(fragmentation) 관련 필드가 삭제
  * 체크섬 (checksum) 필드 삭제
* 트래픽을 효율적으로 관리
  * FlowLabel 필드 활용
* 보안기능
  * 확장헤더를 활용한 종단간 암호화 제공(IPsec)
* 자동 주소설정
  * 로컬 IPv6주소를 LAN상의 MAC주소와 라우터가 제공하는 네트워크 프리픽스(prefix)에 결합하여 IP주소를 자동 생성

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

* 거리벡터 알고리즘에 기초하여 개발된 라우팅 프로토콜
* 최대 15 홉
* 벨만포드 알고리즘 활용


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

### 서브넷마스크

> **네트워크 영역을 늘리고 호스트 영역을 줄일 수 있음**

* IP주소와 서브넷마스크를 논리 AND 연산하면 서브넷네트워크를 구할 수 있다.
* 예시로 155.16.32.* , 155.16.33.* 은 원래 동일 네트워크지만 서브넷을 통해 다른 네트워크로 구성할 수 있다.

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

### Port number

* (1) TCPMUX : TCP Port service multiplexer
* (7) ECHO 
* (20) FTP - DATA : FTP 데이터전송
* (21) FTP - CONTROL : FTP 전송 제어
* (22) SSH
* (23) TELNET : 암호화되지 않은 텍스트 통신
* (25) SMTP 
* (53) DNS
* (69) TFTP 
* (80) HTTP
* (88) Kerberos
* (110) POP3
* (123) NTP : Network Time Protocol, 시간 동기화 프로토콜
* (143) IMAP
* (161) SNMP
* (179) BGP
* (443) HTTPS

---

### 국제표준

**IMT**

* IMT-2000 : 3G 네트워크
* IMT-Advanced : 4G, LTE 네트워크
* IMT-2020 : 5G 네트워크

---

### 



