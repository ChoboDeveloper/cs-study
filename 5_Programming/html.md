# HTML

<br>

**Form**

* 사용자 입력을 서버로 전송하기 위해 사용하는 태그

* 속성

  * action : 폼을 전송할 서버 스크립트 쪽 파일

  * name : 폼을 식별하기 위한 이름

  * accept-charset : 폼 전송에 사용할 문자 인코딩 방식(UTF-8 등)

  * target

  * method : http 메소드

  * enctype : enctype 속성은 폼 데이터(form data)가 서버로 제출될 때 해당 데이터가 인코딩되는 방법을 명시하며 이 속성은 form 요소의 method 속성값이 “post”인 경우에만 사용할 수 있다.

    |              속성값               |      |                             설명                             |
    | :-------------------------------: | :--: | :----------------------------------------------------------: |
    | application/x-www-form-urlencoded |      | 기본값으로, 모든 문자들은 서버로 보내기 전에 인코딩됨을 명시함. |
    |        multipart/form-data        |      | 모든 문자를 인코딩하지 않음을 명시함.이 방식은 <form> 요소가 파일이나 이미지를 서버로 전송할 때 주로 사용함. |
    |            text/plain             |      | 공백 문자(space)는 "+" 기호로 변환하지만, 나머지 문자는 모두 인코딩되지 않음을 명시함. |

---

### WEB

* XML
  * 브라우저간 HTML 호환문제 해결
  * 다목적 마크업 언어
* SOAP(Simple Object Access Protocol)
  * HTTP, SMTP등을 이용하여 XML을 교환하기 위한 프로토콜
  * SOAP는 보통의 경우 원격 프로시저 호출(RPC)을 하는 메시지 패턴을 사용한다.
  * 네트워크 노드(클라이언트)에서 다른 쪽 노드(서버)로 메시지를 요청하고, 서버는 메시지를 즉시 응답하게 된다.
* WSDL(Web Service Description Lang)
  * 웹서비스 관련 서식, 프로토콜을 표준적으로 기술하기 위한 언어
  * XML로 작성되며, UDDI의 기초
* UDDI(Universal Description, Discovery and Integration)
  * 웹서비스에 대한 정보인 WSDL을 등록하고 검색하기 위한 저장소로 공개적으로 접근, 검색이 가능한 레지스터리이자 표준.
  * UDDI는 WSDL로 기술된 웹 서비스 인터페이스의 디렉토리


---

