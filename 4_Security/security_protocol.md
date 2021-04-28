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
* 모드
  * 전송모드
    * 헤더와 페이로드 사이에 AH/ESP가 위치한다.
  * 터널모드
    * 전체 패킷 앞에 AH/ESP가 위치하고 새로운 IP헤더로 데이터를 감싼다.

* SA(Security Association)
  * IPsec을 이용해 보안 통신을 하기 위하여 종단점 끼리 맺는 보안 세션
  * 단방향이므로 2개의 SA 필요
  * SPI(Security Parameter Index), 목적지 IP, 보안 프로토콜 식별자(AH/ESP) 등으로 구성

참고) 2계층에서 터널링 = PPTP, L2TP, L2F / 3계층에서 터널링 = IPsec

---

### SSL/TLS Protocol stack

![image](https://user-images.githubusercontent.com/75229881/111439655-eee03c00-8748-11eb-8a7c-4e67b1ec22b2.png)

* 상위 프로토콜 : Handshake 관련
* 하위 레코드 프로토콜 : 단편화,압축,무결성,암호화 기능관련

**Change Cipher Spec Protocol**

> handshake 과정을 통해 협상된 암호 사양을 새로운 값으로 변경

**Alert Protocol**

>  Handshake 과정에서 오류 발생시 상대방에게 통보 기능 수행

**Record Protocol**

> 상위의 Handshake 프로토콜들의 메세지와 Application 메시지를 수납하여, 레코드 단위로 운반한다. 그리고 분할, 압축, 무결성, 인증등의 기능을 제공한다.

* 데이터를 동일한 크기의 블록으로 단편화(Fragmentation)
* 각 블록을 압축(Compression)
* 각 블록마다 MAC(Message Authentication Code) 생성
* 각 블록+MAC을 암호화(Encryption)
* SSL Record Protocol 헤더 추가

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

### Port number

* (1) TCPMUX : TCP Port service multiplexer
* (7) ECHO 
* (20) FTP - DATA : FTP 데이터전송
* (21) FTP - CONTROL : FTP 전송 제어
* (22) sFTP - SSH + FTP
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

### HTTP 상태코드

**4XX: Client error**

- 400 Bad Request
  - 클라이언트가 올바르지 못한 요청을 보내고 있음을 의미
- 401 Unauthorized
  - 요청을 위해서는 권한 인증등을 요구함을 의미
- 403 Forbidden
  - 요청이 서버에 의해 거부 되었음을 의미, 서버는 거부 이유를 포함하여 응답할 수 있지만, 보통은 거부 이유를 숨기고 싶을 때 사용된다.
- 404 Not Found
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

* 500 Internal Server Error

  * 서버에 오류가 발생하여 응답 할 수 없음
* 501 Not Implemented

  * 클라이언트 요청에 대한 서버의 응답 수행 기능이 없음을 의미(ex] 서버가 지원하지 않는 새로운 Method를 사용하여 요청 - GET2, POST2...)
* 502 Bad Gateway

  * 서버가 게이트웨이로부터 잘못된 응답을 수신했음을 의미합니다. 인터넷상의 서버가 다른 서버로부터 유효하지 않은 응답을 받은 경우 발생
* 503 Service Unavailable

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

