# 네트워크

<br>

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



