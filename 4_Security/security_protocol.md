# 정보보안/프로토콜



### IPSEC

네트워크 계층에서 인증, 기밀성, 키 관리 기능을 제공

* AH(Authentication Header)
  * 정보의 **인증**, **무결성**을 제공한다.
* ESP(Encapsulation Security Payload)
  * IP 페이로드를 암호화하여 **기밀성, 인증, 무결성**을 제공
* IKE(Internet key Exchange)
  * 키 교환에 사용되는 프로토콜이며 UDP 500 포트를 사용
  * 대칭키 교환을 위해 DH를 활용한 IKE를 사용
* 헤더모드
  * 전송모드
    * 헤더와 페이로드 사이에 AH/ESP가 위치한다.
  * 터널모드
    * 전체 패킷 앞에 AH/ESP가 위치하고 새로운 IP헤더로 데이터를 감싼다.
* SA(Security Association)
  * IPsec을 이용해 보안 통신을 하기 위하여 종단점 끼리 맺는 보안 세션
  * 단방향이므로 2개의 SA 필요
  * SPI(Security Parameter Index), 목적지 IP, 보안 프로토콜 식별자(AH/ESP) 등으로 구성

참고) 2계층에서 터널링 = PPTP, L2TP, L2F / 3계층에서 터널링 = IPsec

<br>

**IPSEC VPN 절차**

* 모드1 - ISAKMP SA

  1. SA 제안 - 사용할 암호화 및 인증 알고리즘을 제안 
  2. DH group 교환 - Diffie-Hellman 공개 키와 기타 데이터를 전달
  3. ISAKMP 세션을 인증. IKE SA가 설정되면 IPSec 협상(빠른 모드)이 시작

  * ISAKMP
    * **Hash** : 인증 정보 교환 시 인증 정보가 변질되지 않았음을 증명하기 위한 해쉬 코드 첨부에 사용되는 해쉬 알고리즘
      (MD5, SHA)
    * Authentication : 상대방 VPN을 인증하기 위한 방법
      (Pre-shared Key, RSA Encryption, RSA Signature)
    * **DH(Diffie-Hellman) Group** : 인증 정보를 암호화할 키를 생성하는 대칭키 교환 알고리즘으로 Phase 2에서 사용
      (DH Group 1, DH Group 2, DH Group 5)
    * Lifetime : Phase 1 Tunnel이 유지되는 시간, 다시 말해 새로운 키를 생성하는 주기를 의미
      (통상적으로 86400초)
    * Encryption : 키 교환 알고리즘과 함께 인증 정보를 암호화할 암호화 알고리즘
      (AES, DES, 3DES)

* 모드2 - IPSEC SA

  1. IPSec SA 제안 및 협의
  2. 패킷을 암호화할 암호화 키 생성 및 인증

  * IPSEC
    * **IPSec Protocol** : 패킷 인증/암호화를 위한 프로토콜 헤더 선택
      (AH / ESP)
    * **Encapsulation Mode** : IPSec 터널의 운용 모드 선택
      (Transport / Tunnel)
    * Encryption : 패킷을 암호화할 암호화 알고리즘 선택
      (AES, DES, 3DES)
    * Authentication : 패킷을 인증할 해쉬 알고리즘 선택
      (MD5, SHA)
    * Lifetime : Phase 2 Tunnel이 유지되는 시간, 다시 말해 Phase 1의 대칭키를 기반으로 키를 재생성하는 주기를 의미

---

### SSL/TLS Protocol stack

> **단편화->압축->MAC->암호화->전송**
>
> 부인방지X

![image](https://user-images.githubusercontent.com/75229881/111439655-eee03c00-8748-11eb-8a7c-4e67b1ec22b2.png)

* 상위 프로토콜 : Handshake 관련
* 하위 레코드 프로토콜 : 단편화,압축,무결성,암호화 기능관련

**Change Cipher Spec Protocol**

> handshake 과정을 통해 협상된 암호 사양을 새로운 값으로 변경

**Alert Protocol**

>  Handshake 과정에서 오류 발생시 상대방에게 통보 기능 수행

**Record Protocol**

> 상위의 Handshake 프로토콜들의 메세지와 Application 메시지를 수납하여, 레코드 단위로 운반한다. 그리고 분할, 압축, 무결성, 인증등의 기능을 제공한다.

1. 데이터를 동일한 크기의 블록으로 **단편화(Fragmentation)**
2. 각 블록을 **압축(Compression)**
3. 각 블록마다 **MAC(Message Authentication Code)** 생성
4. 각 블록+MAC을 **암호화(Encryption)**
5. SSL Record Protocol 헤더 추가

---

### SSL/TLS Handshake

1. **Client Hello**
   * 클라이언트가 서버에 Client Hello 메시지 전송
   * SSL/TLS version, 지원하는 cipher suite, 세션 ID, Random 바이트
2. **Server Hello**
   * 서버가 클라이언트에 Server Hello 메시지 전송
   * 내용은 위와 동일, cipher suite 선택
3. **Certificate**
   * 서버의 Certificate를 클라이언트에게 전송
   * 만약 서버가 클라이언트에게 인증서를 요청하였다면, 클라이언트는 인증서를 서버에게 전송(Optional)
4. **Server Key Exchange / Server Hello Done**
   * (Server Key Exchange) Server의 공개키가 SSL 인증서 내부에 없는 경우, Server가 직접 전달함을 의미
   * (Server Hello Done) 인증서 내부에 공개키가 있다면 Client가 CA(Certificate Authority, 인증기관)의 공개키를 통해 인증서를 복호화한 후 Server의 공개키를 확보
     * (참고) Server의 인증서는 CA에 의해 암호화되어 신뢰성을 보장받고 있음
5. **Client Key Exchange**
   * (RSA) SSL 인증서 내부의 공개키로 암호화한 대칭키를 Client가 생성하여 Server에 전달
   * (DH, DHE,ECDHE) Client가 데이터를 암호화할 대칭키를 보내는 것이 아니라 대칭키를 생성할 재료(Pre-Master Secret)를 Client와 Server가 교환. 그리고 서로 교환한 각자의 재료를 합쳐 동일한 대칭키(Master Secret과 Session Key)를 생성
6. **Change Cipher Spec**(Client -> Server)
   * 성공적으로 공유키를 생성했으며, 이후 메시지는 암호화 하여 전송할 것을 알림
7. **Client Finished**
   * 첫 번째, 암호화 된 메세지
8. **Change Cipher Spec**(Server->Client)
9. **Server Finished**

---

### SSL/TLS Certificate

> [SSL과 인증서 구조 이해하기](https://m.blog.naver.com/alice_k106/221468341565)

* Root 인증서는 세상 사람들이 모두 신뢰하기로 약속한 기관, 예를 들어 위에서 언급한 Geotrust 등의 기관에서 발행한 인증서가 된다. 이러한 인증서는 일반적으로 웹 브라우저 등에 미리 내장되어 있으며, 해당 인증서에 대응하는 공개 키 또한 인증서 내부에 포함되어 있다.
* Google CA와 같은 CA회사의 인증서는 이러한 Root 인증서에 요청하여 root 인증서의 개인키를 통해 암호화되어 신뢰성을 보장받는다. 따라서, **Google CA의 인증서의 내용물에 대한 해시 값을, Geotrust가 Geotrust의 비밀 키로 암호화 해준것일테니, Google CA 또한 신뢰할 수 있다.**
* 여기서 해시값은 인증서의 주요정보를 모아 SHA256등의 해쉬 알고리즘을 이용하여 해쉬를 수행하고, 이렇게 해서 나온 해시값을 인증서의 **Finger Print(지문)**이라고 한다. 이렇게 나온 해시값(Finger Print)을 발급자(issuer)(CA)의 개인키로 암호화한 값이 **서명값(Digital Signing)**이다.
* CA의 공개키로 서명값을 복호화했을 때 이러한 해시값의 비교를 통해 해당 인증서의 무결성을 검증할 수 있다.

---

### PFS(Perfect Forward Secrecy)

* DHE 키 교환 알고리즘의 특성을 사용하여 주기적으로 비밀키(대칭키)를 변경하여 특정 기간에는 특정한 비밀키(대칭키)로 데이터를 암호화하는 것을 **Forward Secrecy(FS) 혹은 Perfect Forward Secrecy(PFS)**라고 한다.

* 데이터 교환이 이루어지는 내내 일회용 비밀키(대칭키)를 바꾸어 가면서 사용하는 것. 특정 기간의 비밀키(대칭키)를 탈취당하더라도 피해는 '해당 특정 기간'에만 국한되기 때문에 안전
* 주기적인 키 교환이 가능한 DHE와 ECDHE만이 이 기능을 지원

---

### SNMP

* Manager은 관리 시스템(162/udp), Agent는 관리 대상(161/udp)
* Manager은 Polling, Agent는 Event Reporting

---

### SSH

* 시큐어 셸 프로토콜, 22번 포트
* TCP를 활용하여 안전한 소켓통신 보장
* **전송계층, 인증, 연결 프로토콜**로 구성
  * SSH 전송 프로토콜 (SSH Transport Layer Protocol, SSH TLP)
    - 서버 인증, 기밀성, 무결성, 압축(옵션) 제공
    - 주요 협상 대상 : 키 교환 방식, 공개 키 방식, 대칭 키 방식, 메세지 인증 방식, 해시 알고리즘 등이 클라이언트,서버 간에 협상되어짐
  * SSH 인증 프로토콜 (SSH User Authentication Protocol)
    - 해당 서버에 대한 사용자 인증(User Authentication) 제공
  * SSH 연결 프로토콜 (SSH Connection Protocol)
    - 암호화된 터널들 각각에 다수 논리채널들을 다중화 (1:N) 가능
  * SSH 응용 프로토콜 : TELNET,RLOGIN,SMTP 등

* **한 개의 SSH 연결로 다중화**된 통신채널 운용가능

---

### DTLS

* UDP에서 구현된 SSL

---

### SET

* SECURE ELECTRONIC TRANSACTION

  * SET(Secure Electronic Transaction)는 인터넷을 이용한 전자상거래에서의 안전한 지급 결제를 위하여 비자와 마스터카드사가 공동으로 개발한 신용/직불카드결제를 위한 보안프로토콜
* **SET 참여주체**

  - 고객(Card Holder): 카드 소지자
  - 상점(Merchant): 인터넷상에서 상품이나 정보서비스 제공자
  - 지불중계관(**PG**, Payment Gateway): 판매자가 요청한 고객의 지불정보로 금융기관에 승인 및 결재를 요청하는 자
  - 발급사(Issuer): 고객카드를 발급하고 고객계좌가 개설된 금융기관
  - 매입사(Acquirer): 상점을 가맹점으로 승인하고 상점 계좌가 열린 금융기관
  - 인증기관(CA): 참여 기관에게 전자적인 인증서를 발급하는 기관

* **이중서명**
  * 카드 사용자가 구매정보와 지불정보를 각각 해시한 후, 두 해시값을 합한 뒤 다시 해시하여 이 값을 카드 사용자의 개인키로 암호화하여 이중서명 값을 생성한다.

---



  
