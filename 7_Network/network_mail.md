# 네트워크/전자메일

<br>

### SMTP

* 인터넷 전자우편 표준 프로토콜
* 포트 25, 응용계층
* Store-and-Forward 방식으로 메시지를 전달한다.
* 상대 서버를 지시하기 위해 DNS의 MX 레코드 (Mail Exchanger) 가 사용된다.



<img src = "https://user-images.githubusercontent.com/75229881/116352002-813b2b80-a82f-11eb-834a-03223485803e.png" width="70%">

**구성요소**

* Mail Transfer Agent (MTA)
  * 서버안의 하나의 메일 전송 에이전트
  * (송신 시) 사용자로부터 메일을 전달받아서 외부로 전달해주는 프로그램
  * (수신 시)  외부로부터 MTA가 메일을 수신하면, 적절한 MDA에게 메일을 전달한다.
* Mail Delivery Agent (MDA)
  * 사용자의 메일함으로 메일을 저장해주는 프로그램
  * 외부로부터 수신한 메일을 MTA가 MDA에게 전달해주면, MDA는 해당 사용자의 메일함에다가 저장한다.
* Mail User Agent (MUA)
  * 사용자가 메일 송/수신을 위해 사용하는 클라이언트 프로그램
  * 메일을 작성하거나 메일함에 도착한 메일을 보여주는 기능을 수행한다.
* MRA/MAA
  * 리모트 서버에 있는 우편함으로부터 사용자의 MUA로 메시지를 가져오는 프로그램

---

