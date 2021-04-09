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

