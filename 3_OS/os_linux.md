# UNIX/Linux

<br>

### UNIX 시스템 구성

* Kernel
* Shell
  * 사용자가 명령어를 인식하여 프로그램을 호출하고 명령을 수행하는 명령어 해석기
  * 시스템과 사용자간의 인터페이스 담당
* Utility Program
  * 일반 사용자가 작성한 응용 프로그램을 처리하는데 사용
  * 에디터, 컴파일러, 인터프리터, 디버거 등

---

### IPC

> Inter-Process Communication
>
> UNIX 시스템은 다양한 종류의 프로세스 간 통신을 지원
>
> 각 프로세스는 시스템호출을 통해 커널의 기능을 사용하며, 프로세스간 통신은 Signal, Pipe, Socket 등을 사용한다

* 시그널(Signal) : 간단한 메세지를 이용하여 통신하는 것으로, 초기 UNIX 시스템에서 사용됨
* 파이프(Pipe) : 한 프로세스의 출력이 다른 프로세스의 입력으로 사용되는 단방향 통신 방식
* 소켓(Socket) : 프로세스 사이의 대화를 가능하게하는 쌍방향 통신방식
* 메시지 큐(Message Queue), 공유 메모리(Shared Memory), 세마포어(Semaphore) 등

---

### 파일

* 일반 파일(Regular File)

  * 데이터 또는 프로그램 코드에 해당하는 일련의 바이트 스트림으로 구성
  * 정규 파일은 표준 파일 입출력 시스템 호출을 통해 참조됨
* 디렉토리 파일(Directory File)
  * 다른 파일의 목록 혹은 포인터를 가지는 파일
  * 디렉토리 파일은 디렉토리의 명시적인 시스템 호출을 통해 참조됨

* 특수 파일(Special File)
  * 프린터와 터미널, 디스크 같은 주변 장치나 또는 파이프와 소켓 같은 프로세스 간 상호 통신 기법에 해당
  * 표준 입출력 시스템 호출을 통해 참조됨

---

### 디렉토리 구조

![리눅스 디렉토리 구조](https://t1.daumcdn.net/cfile/tistory/223BDE4855351B370F)

#### /(루트)

최상의 디렉토리인 루트 디렉토리를 의미하며, 리눅스의 모든 디렉토리들의 시작점이다. 즉, 모든 디렉토리들을 절대경로로 표기할 때에 이 디렉토리로부터 시작해야 한다.

#### /bin

기본적인 명령어가 저장된 디렉토리. 즉, 리눅스 시스템사용에 있어 가장 기본적이라고 할 수 있는 mv, cp, rm 등과 같은 명령어들이 이 디렉토리에 존재하며 root 사용자와 일반사용자가 함께 사용할 수 있는 명령어 디렉토리이다.

#### /etc

시스템의 거의 모든 설정파일이 존재하는 디렉토리. /etc/sysconfig(시스템 제어판용 설정파일), /etc/passwd(사용자관리 설정파일), /etc/named.conf(DNS 설정파일) 등과 같은 파일들이 존재한다.

#### /etc/crontab

리눅스에서는 일반적으로 cron 데몬이 주기적인 작업 실행을 처리한다. cron이 시작될 때부터 끝날 때까지 계속 실행되며 실행되며 cron 설정 파일은crontab이라 부른다.

#### /home

사용자의 홈디렉토리, useradd 명령어로 새로운 사용자를 생성하면 대부분 사용자의 ID와 동일한 이름의 디렉토리가 자동으로 생성됨

#### /lib

커널모듈파일과 라이브러리파일 즉, 커널이 필요로하는 커널모듈파일들과 프로그램(C, C++ 등)에 필요한 각종 라이브러리 파일들이 존재하는 디렉토리

#### /proc

일명 "가상파일시스템" 이라고 하는 곳으로 현재 메모리에 존재하는 모든 작업들이 파일형태로 존재하는 곳이다. 디스크상에 실제 존재하는 것이 아니라 메모리상에 존재하기 때문에 가상파일시스템이라고 부른다. 실제 운용상태를 정확하게 파악할 수 있는 중요한 정보를 제공하며 여기에 존재하는 파일들 가운데 현재 실행중인 커널(kernel)의 옵션 값을 즉시 변경할 수 있는 파라미터파일들이 있기 때문에 시스템 운용에 있어 매우 중요한 의미를 가진다.

#### /usr

시스템이 아닌 일반사용자들이 주로 사용하는 디렉토리. 즉, c++, chsh, cpp, crontab, du, find등과 같이 일반사용자들용 명령어들은 /usr/bin 에 위치한다.

#### /usr/bin/

일반 사용자들이 사용가능한 명령어 파일들이 존재하는 디렉토리

#### /var

시스템운용중에 생성되었다가 삭제되는 데이터를 일시적으로 저장하기 위한 디렉토리. 거의 모든 시스템로그파일은 /var/log 에 저장되고, DNS 의 zone 설정파일은 /var/named 에 저장되고, 메일파일은 /var/spool/mail 에 저장되며, 크론설정파일은 /var/spool/cron 디렉토리에 각각 저장됨

#### /var/log/

시스템로그파일(messages, secure, xferlog 파일등)이 저장되는 디렉토리

---

### 기본 명령어

* ls(List) : 파일이나 디렉토리 정보 출력
* pwd(print work directory) : 작업중인 디렉토리 확인
* cd : 이동
* mkdir(Make Directory) : 디렉토리 생성
* rmdir : 디렉토리 삭제
* cat : 파일 내용 출력
* cp : 복사
* touch : 파일의 접근 및 수정 시간 변경
* tail : 로그파일 변경을 실시간으로 확인가능
* find : 파일, 디렉토리 검색

---

### 권한 명령어

* ls -al
  * 모든 파일의 퍼미션정보를 볼 수 있음
  *  d/rwx/rwx/rwx 여기서 d 다음으로 순서대로 소유자, 그룹, 일반유저에 대한 권한
  * 맨 앞글자 d는 디렉토리(폴더), -는 일반파일
* chown : 파일 및 디렉토리의 소유권을 바꾸는 명령어

  * chown [옵션] [소유권자:그룹식별자] [파일명]
  * 하위 사용자는 최고 권한 사용자인 root에게 권한부여를 할 수 없다. (소유자 변경도 마찬가지)
  * 예제
    *  chown member1 test.c (파일에 대해 소유자를 member1로 바꾼다)
    *  chown :member1 test.c (파일에 대해 그룹을 members1로 바꾼다)
    *  chown member1: test.c (파일에 대해 소유자 및 그룹을 members1로 바꾼다.)
    *  chown member1:member2 test.c (파일에 대해 소유자는 member1, 그룹은 member2로 바꾼다)
* chmod : 파일, 디렉토리의 권한을 변경하는 명령어
  * chmod [권한값] [파일명]
  * **u**ser, **g**roup, **o**thers, **a**ll
  * +는 권한 부여, -는 권한 취소
  * 예제
    * chmod **g+w** test.c (그룹에 쓰기 권한을 준다)
    * chmod **o-r** test.c (기타사용자에게 읽기 권한을 빼앗는다)
    *  chmod **707** test.c (user, other 은 모두 rwx로 변경하고 group은 모든 권한을 제거)
  * 특수권한
    - 4777= SetUid 설정 때 4000을 더함
    - 2777= SetGid 설정 때 2000을 더함
    - 1777= Sticky bit 설정 때 1000을 더함
    - chmod **u+s** test.c 처럼 사용가능
    - setUid시 실행권한이 있으면 s표기, 없으면 S표기
* umask : 새로 만들어진 파일에 파일 권한을 어떻게 설정할지를 제어하는 마스크 설정을 결정하는 명령어

  * 디렉토리=777, 파일=666 에서 umask값을 뺀다
* **grep** : 파일 내 정규표현식을 포함한 모든 행을 검색 및 출력하는 명령어
  *  파일의 내용이나 콘솔에 출력물 중에 특정 문자열을 찾는데 널리 사용된다.
* **find** : 원하는 조건의 파일, 디렉토리 모든 것을 검색한다.

---

### 로그 명령어

* /var/log/messages
  * 로그 파일중 가장 중요하고 기본적인 부분으로 시스템이 운영되는 전반적인 내용이 기록되는 파일
  * 로그인 기록부터 디바이스 정보 , 시스템 설정오류 , 파일 시스템 , 네트워크 세션기록 등 주로 시스템 데몬들의 실행상황과 내역, 그리고 사용자들의 접속정보
*  /var/log/secure
  * 최근 서버 접속자 기록
  * 텍스트 파일로 **grep** 명령어 사용
* /var/log/**lastlog**
  * /etc/passwd에 존재하는 모든 계정을 대상으로 하여 언제 마지막으로 서버에 접속을 했는지를 확인
  * Mail, adm, bin 등의 계정들은 모두 Never logged in
* /var/log/**wtmp**
  * 최근 로그인/로그아웃 정보, 시스템의 Boot/Shutdoun 정보에 대한 누적정보
  * **last** 명령어 사용
* /var/log/**utmp**
  * 현재 로그인한 사용자의 상태정보를 담고 있는 파일
  * **w,who,finger**등의 명령어 사용
* /var/log/**btmp**
  * 실패한 로그인 시도에 대한 기록을 담고 있는 파일
  * **lastb** 명령어 사용
* /var/account/**pacct**
  * 사용자별 명령실행 정보
  * binary 파일로 내용 확인시 **lastcomm** 명령어 사용
* /var/log/xferlog
  * FTP 로그파일
* /etc/passwd
  * 계정정보 및 패스워드 파일
  * pwconv 명령어로 shadow 활성화 / pwunconv 비활성화
* /etc/shadow
  * 암호화된 패스워드 파일
  * abcd:$Hashid$Salt$Hash vlaue:17562:0:99999:7:3::과 같이 구성
    * abcd : 사용자의 계정명
    * Hashid : MD-5 : $1, SHA-256 : $5, SHA-512 : $6
    * 17562 : 최종수정일을 70년기준으로 계산
    * 0 : 암호최소사용일, 0일만큼 비밀번호 유지해야함
    * 99999 : 최대사용일, 99999만큼 변경안해도 됌
    * 7 : 만료경고일, 만료 7일전부터 경고
    * 3 : 만료 유예기간 이후에는 로그인 불가

---

### 시그널

* 프로세스 간 통신
* 비동기식 통신

| **번호** | **이름**       | **설명**                                                     | **기본 처리**  |
| -------- | -------------- | ------------------------------------------------------------ | -------------- |
| 1        | SIGHUP(HUP)    | HangUP의 약어로 로그아웃과 같이 터미널에서 접속이 끊겼을 때 보내지는 시그널입니다. | 종료           |
| 2        | SIGINT (INT)   | 키보드로부터 오는 인터럽트 시그널로 실행을 중지              | 종료           |
| 3        | SIGQUIT (QUIT) | 키보드로부터 오는 실행 중지 시그널                           | 코어 덤프      |
| 4        | SIGILL (ILL)   | illegal instruction의 약자입니다. 잘못된 명령을 사용했을 때 발생합니다. | 코어 덤프      |
| 5        | SIGTRAP (TRAP) | trace(추적), breakpoint(중지점)에서 TRAP 발생할 때           | 코어 덤프      |
| 6        | SIGABRT (ABRT) | abort의 약자로 비정상종료 함수에 의해 발생합니다. (즉 abort 시스템 호출을 하였을 때 발생) | 코어 덤프      |
| 7        | SIGBUS         | 메모리 접근 에러시 발생하는 시그널입니다.                    | 코어 덤프      |
| 9        | SIGKILL (KILL) | KILL! 무조건 종료, 즉 프로세스를 강제로 종료시키는 시그널!   | 종료           |
| 11       | SIGSEGV        | invalid memory reference                                     | 종료 +코어덤프 |
| 15       | SIGTERM (TERM) | Terminate의 약자로 가능한 정상 종료시키는 시그널로 kill 명령의 기본 시그널입니다. | 종료           |
| 17       | SIGCHLD(child) | 자식 프로세스가 stop 되거나 종료되었을 때 부모에게 전달되는 신호입니다. (멀티 프로세스 코딩에서 자세한 사용법은 배울 거..) | 무시           |
| 18       | SIGCONT (CONT) | Continue의 약자로 STOP 시그널에 의해 정지된 프로세스를 다시 실행시킬 때 사용됩니다. | 재시작         |
| 19       | SIGSTOP (STOP) | 터미널에서 입력된 정지 시그널입니다. SIGCONT로 재실행시킬 수 있습니다. | 중지           |
| 20       | SIGTSTP (TSTP) | 실행 정지 후 다시 실행을 계속하기 위해 대기시키는 시그널입니다.[CTRL] + [z]를 입력했을 때 보내지는 시그널입니다.SIGCONT로 역시 다시 실행시킬 수 있습니다. | 중지           |
| 29       | SIGIO          | 비동기 입출력이 발생했을 경우 ! (I/O now possible!)          | 종료           |

---

### 프로세스

* PID 1은 init 프로세스, 0은 특별한 목적으로 예약된 번호로 유휴 프로세스에 지정
* PID는 ps명령어를 통해 확인가능
  * PPID(부모의 PID)와 UID(사용자의 ID)까지 확인하기 위해 자세한 정보를 출력하기 위해서는 ps -f 사용
* fork()
  * 자식 프로세스 생성 성공 시 0, 실패시 -1 리턴
  * 부모 프로세스라면 양수를 리턴한다.

---





