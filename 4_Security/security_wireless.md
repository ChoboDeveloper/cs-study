# 보안/무선랜



### WEP

* 초기 무선랜 보안기술
* 고정된 공유키와 무작위로 생성한 초기 벡터(IV)를 조합한 키를 이용한 RC4알고리즘 기반의 데이터 암호화
* IV : 24bit
* 공유키 : 40bit
* 기밀성 : RC-4
* 무결성 : CRC-32

---

### WPA

* TKIP은 WEP을 SW적으로 확장한 것, TKIP로 암호키 동적변경
* IV를 48bit로 늘렸지만 RC4 알고리즘의 취약점은 그대로 갖고 있음
* 공유키 : 128bit, PSK
* 기밀성 : RC4-TKIP
* 무결성 : 메시지 인증 코드(MAC)

---

### WPA2

* 공유키 : AES기반의 128bit 대칭키 사용, PSK
* 기밀성 : AES-CCMP
* 무결성 : CBC-MAC

---

#### WPA/WPA - Enterprise

* WPA-PSK가 기존 WEP의 암·복호화 키 관리 방식을 중점적으로 보완한 방식인데 비해서 WPA-Enterprise는 사용자 인증영역까지 보완한 방식
* EAP/Radius 프로토콜을 채택
* 즉, WPA/WPA2 의 PSK 버전은 사용자 인증을 거치지 않고 WEP 처럼 AP 와 사용자가 같은 Key를 공유하고, 그 키를 보호함으로써 이루어지는 방식인데 반해, Enterprise 버전은 사용자 인증을 거치게 함으로써(EAP 인증 프로토콜) 더 안전하게 통신할 수 있는 것이다. 하지만 이러한 인증 담당할 서버(Radius)를 따로 구성하여야만 WPA/WPA2-EAP 를 이용할 수 있으므로 보통 대규모 기업이나 보안이 중요한 곳에서 사용한다.

---

### IEEE 802.1X

* 인증을 통해 네트워크를 보호하는 포트 기반의 접근제어 가능하게 하는 인증구조
* 유무선 네트워크 모두 적용 가능(현재는 WLAN 접속방식에 주로 활성화)
* 단말 인증보다 사용자 인증 위주

인증 프로세스에서 802.1X 인증이 적용된 AP에게 연결 요청
이 때, 기본적으로 EAP(Extensible Authentication Protocol) 요청

---

### EAP(Extensible Authentication Protocol)

* 확장형 인증 프로토콜

- IEEE 802.1X에서 사용자 인증 방법으로 사용
- 어떤 링크에서도 접속 가능한 단순한 캡슐화 개념의 프로토콜

---

###  RADIUS

> 대규모 고객을 관리하는 시스템에서 AP에 사용자가 인증한 정보가 유효한지 Radius 서버가 가진 정보와 비교한다

* 인증서버

- Network 자원을 제공하는 NAS(Network Access Service) 장비가 중앙의 인증서버와 인증을 통한 사용 권한 부여, 설정된 정보, 접속 사용시간 및 각종 기록 정보를 공유하기 위해 정의된 프로토콜
- 대표적인 AAA(Authentication, Authorization, Accounting) 서버
- AP와 RADIUS Server 사이에는 사전에 공유된 키를 이용하여 인증
- RADIUS 서버 없이 운영시, AP등의 access 개체가 모두 모든 사용자 정보 가지고 있어야 하며 각 개체가 가지고 있는 사용자 정보 동기화 필요

---



