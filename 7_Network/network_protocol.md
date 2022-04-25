# 네트워크 프로토콜

<br>



### ICMP

> Internet Control Message Protocol, 네트워크 계층 프로토콜

* ICMP 메세지들은 일반적으로 IP 동작에서 진단이나 제어로 사용되거나 오류에 대한 응답으로 만들어진다
* ICMP 오류들은 원래 패킷의 소스 IP 주소로 보내지게 된다
* ICMP 활용 명령어
  * Ping : 상대방 호스트의 작동 여부 및 응답시간 측정하는데 사용
    * ICMP TPYE 8(ECHO Request)를 보내면 ICMP TYPE 0(ECHO Reply)를 회신받는다.
    * ICMP TYPE 3(**Destination Unreachable**) : ECHO Request에 응답이 없는경우
    * ICMP TYPE 11(Time Exceeded) : TTL이 0인 경우
  * Tracert : 목적지까지의 라우팅 경로 추적을 하기 위해 사용
    * 참고) Traceroute는 리눅스 명령어이며 비슷한 기능을 하지만 UDP를 사용한다.

---

### FTP

* 포트 20(데이터 전송), 21(제어신호 전송)
* File Transfer Protocol
* FTPS = FTP + SSL
* sFTP = FTP + SSH (22번 포트)
* SSL은 TCP/IP의 암호화, SSH는 Telnet(원격접속), 데이터전송 암호화

**Mode**

* Active
  * 클라이언트가 포트 열고 서버에게 알림
* Passive
  * 서버가 포트를 알려줌

---

### HTTP

**URL 구성**

| 형식      | 구성요소  | URL주소                |
| --------- | --------- | ---------------------- |
| schema:// | protocol  | http://                |
| authority | host      | codedragon.tistory.com |
| port      | port      | :80                    |
| path?     | path      | /member/mem.jsp        |
| query#    | query     | ?name=hong#            |
| fragment  | reference | content                |

**HTTP의 특징**

* 비연결성
  * 클라이언트의 요청에 서버가 응답하면 연결을 끊어버림
  * 연결을 유지하기 위한 리소스를 줄일 수 있지만 다수의 연결/해제에 따른 오버헤드가 발생한다
  * HTTP 1.0 기준으로비연결성을 해결하기 위해 KeepAlive 속성을 사용 - 클라이언트의 응답상태를 주기적으로 확인
  * HTTP 1.1기준으로 연결성을 가지고 TimeOut을 통해 관리
* Stateless
  * 서버는 클라이언트의 상태를 모른다. 정보유지 X
  * 브라우저에서 쿠키, 서버에서 세션을 통해 해결

---

### DHCP

> Dynamic Host Configuration Protocol
>
> 호스트의 IP주소와 각종 TCP/IP 프로토콜의 기본 설정을 클라이언트에게 자동적으로 제공해주는 프로토콜

**특징**

* DHCP 서버로부터 클라이언트들이 필요한 IP를 임대받고 TCP/IP 설정을 자동으로 받을 수 있다.

* DHCP를 통한 IP 주소 할당은 “임대”라는 개념을 가지고 있는데 이는 DHCP 서버가 IP 주소를 영구적으로 단말에 할당하는 것이 아니고 임대기간(IP Lease Time)을 명시하여 그 기간 동안만 단말이 IP 주소를 사용하도록 하는 것이다.
* 단말은 임대기간 이후에도 계속 해당 IP 주소를 사용하고자 한다면 IP 주소 임대기간 연장(IP Address Renewal)을 DHCP 서버에 요청해야 하고 또한 단말은 임대 받은 IP 주소가 더 이상 필요치 않게 되면 IP 주소 반납 절차(IP Address Release)를 수행하게 된다.

**DHCP 메세지**

* DHCP Discover
  * 단말이 DHCP 서버를 찾기 위해 메세지를 보냄
* DHCP Offer
  * DHCP 서버의 응답으로 단순히 DHCP 서버의 존재만을 알리지 않고, 단말에 할당할 IP 주소 정보를 포함한 다양한 "네트워크 정보"를 함께 단말에 전송
  * 네트워크 정보 : (IP , subnet mask, default gateway 등)
* DHCP Request
  * 이제 단말은 DHCP Request 메시지를 통해 하나의 DHCP 서버를 선택하고 해당 서버에게 MAC 주소를 보내고 "단말이 사용할 네트워크 정보"를 요청
* DHCP ACK
  * DHCP 절차의 마지막 메시지로, DHCP 서버가 단말에게 "네트워크 정보"를 전달해 주는 메시지로 앞서 설명드린 DHCP Offer의 '네트워크 정보"와 동일한 파라미터가 포함된다.

---

### TCP

* 제어플래그

  | URG | ACK | PSH | RST | SYN | FIN |

  * **SYN(Synchronization:동기화) - S : 연결 요청 플래그**
    * TCP에서 세션을 성립할 때 가장 먼저 보내는 패킷
    * 시퀀스 번호를 임의적으로 설정하여 세션을 연결하는 데에 사용되며 초기에 시퀀스 번호를 보내게 된다.

   

  * **ACK(Acknowledgement) - Ack : 응답**
    * 상대방으로부터 패킷을 받았다는 걸 알려주는 패킷, 다른 플래그와 같이 출력되는 경우도 있습니다.
    * 받는 사람이 보낸 사람 시퀀스 번호에 TCP 계층에서 길이 또는 데이터 양을 더한 것과 같은 ACK를 보냅니다.(일반적으로 +1 하여 보냄)
    * ACK 응답을 통해 보낸 패킷에 대한 성공, 실패를 판단하여 재전송하거나 다음 패킷을 전송한다.

   

  * **PSH(Push) - P : 밀어 넣기**
    * TELNET과 같은 상호작용이 중요한 프로토콜의 경우 빠른 응답이 중요한데, 이때 받은 데이터를 즉시 목적지인 OSI 7 Layer의 Application 계층으로 전송하도록 하는 FLAG.
    * 대화형 트래픽에 사용되는 것으로 버퍼가 채워지기를 기다리지 않고 데이터를 전달한다.
    * 데이터는 버퍼링 없이 바로 위 계층이 아닌 7 계층의 응용프로그램으로 바로 전달한다.

   

  * **RST(Reset) - R : 재 연결 종료**
    * 재설정(Reset)을 하는 과정이며 양방향에서 동시에 일어나는 중단 작업이다.
    * **비 정상적인 세션 연결 끊기**에 해당한다.
    * 이 패킷을 보내는 곳이 현재 접속하고 있는 곳과 즉시 연결을 끊고자 할 때 사용한다.

  

  * **URG(Urgent) - U : 긴급 데이터**
    * Urgent pointer 유효한 것인지를 나타낸다. 
    * Urgent pointer란 전송하는 데이터 중에서 긴급히 전달해야 할 내용이 있을 경우에 사용한다. 
    * 긴급한 데이터는 다른 데이터에 비해 우선순위가 높아야 한다. ex) ping 명령어 실행 도중 Ctrl+C 입력

  * **FIN(Finish) - F : 연결 종료 요청**
    * 세션 연결을 종료시킬 때 사용되며 더 이상 전송할 데이터가 없음을 나타낸다.

---

### MQTT

* IOT를 위한 프로토콜로서, 최소한의 전력과 패킷량으로 통신하는 프로토콜
*  IOT와 모바일 어플리케이션 등의 통신에 매우 적합한 프로토콜
* Publisher, Broker, Subscriber로 구성

---

### RPC

> 원격 프로시저 프로토콜, 111

* 정의
  * 원격 프로시저 호출(영어: remote procedure call, 리모트 프로시저 콜, RPC)은 별도의 원격 제어를 위한 코딩 없이 다른 주소 공간에서 함수나 프로시저를 실행할 수 있게하는 프로세스 간 통신 기술이다. 다시 말해, 원격 프로시저 호출을 이용하면 프로그래머는 함수가 실행 프로그램에 로컬 위치에 있든 원격 위치에 있든 동일한 코드를 이용할 수 있다.
  * 일반적으로 프로세스는 자신의 주소공간안에 존재하는 함수를 호출하여 실행가능하지만, RPC를 이용하면 다른 주소공간에서 동작하는 프로세스의 함수를 실행할 수 있게 된다.
* 왜?
  * 현재 유행하는 `MSA(Micro Service Architecture)` 구조로 서비스를 만들다보면, 다양한 언어와 프레임워크로 개발되는 경우가 잦음. 이런 `Polyglot` 한 구조에서는 프로토콜(Socket)을 맞춰서 통신해야 하는 비용이 발생한다.
  * **통신 관련 문제를 신경 쓰지 않고 원격지의 함수를 마치 로컬의 함수처럼 쓴다**는 것이 큰 장점이다. 특히, **IDL(Interface Definication Language)** 기반으로 다양한 언어를 가진 환경에서도 쉽게 확장이 가능
  * 이 경우에 RPC를 이용하여 언어에 구애받지 않고, 원격에 있는 프로시저를 호출하여 조금 더 비즈니스 로직에 집중하는 개발을 할 수 있다.



---

### Port number

* (1) TCPMUX : TCP Port service multiplexer
* (7) ECHO 
* (20) FTP - DATA : FTP 데이터전송
* (21) FTP - CONTROL : FTP 전송 제어
* (22) SSH
* (23) TELNET
* (25) SMTP 
* (53) DNS
* (69) TFTP 
* (80) HTTP
* (88) Kerberos
* (110) POP3
* (123) NTP : Network Time Protocol, 시간 동기화 프로토콜
* (143) IMAP
* (UDP, 161) SNMP
* (179) BGP
* (443) HTTPS

---

