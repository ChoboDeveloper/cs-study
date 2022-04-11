# Window

<br>

### 레지스트리

**하이브**

> 레지스트리를 분류하는 섹션

* HKEY_CLASSES_ROOT
  * 확장자에 관련된 정보와 연결 프로그램 정보
* HKEY_CURRENT_USER
  * 현재 로그인한 사용자의 설정
* HKEY_LOCAL_MACHINE
  * 시스템에 설치된 소프트웨어와 하드웨어에 대한 정보, 운영체제에 관련된설정, 서비스 및 보안 관련 설정 등의 방대한 정보를 저장
* HKEY_USERS
  * 시스템에 있는 모든 사용자와 그룹의 계정에 관련된 정보를 저장
* HKEY_CURRENT_CONFIG
  * LOCAL_MACHINE의 하위 키로 해당 CONFIG 정보
  * 디스플레이 설정, 폰트, 프린터 설정 등
* HKEY_DYN_DATA
  * 플러그 앤 플레이, 하드웨어의 변화 등

---

### 윈도우 인증

**LSA(Local Security Authority)**

* 모든 계정의 로그인 검증 및 접근권한 검사
* **로컬보안정책**을 집행한다

**SAM(Security Account Manager)**

* 사용자/그룹 계정정보에 대한 데이터베이스 관리

**SRM(Security Reference Monitor)**

* 인증된 **사용자에게 SID 부여**
* Secuirty ID를 바탕으로 접근제어

---

### 시스템 프로세스

**System.exe**

* 네트워크 입출력, 디스크 입출력 및 실제 커널 자체를 처리한다.

**Csrss.exe**

* Windows 콘솔을 관리하고 커널모드의 드라이버와 쓰레드를 생성, 삭제하는 프로세스

**Smss.exe**

* 사용자 세션을 시작하는 기능을 담당한다. 이 프로세스는 winlogon, Win32(csrss.exe)를 구동시키고, 시스템 변수를 설정한다. 또한 winlogon이나 csrss가 끝나기를 기다려 정상적인 winlogon과 csrss 종료 시 시스템을 종료시킨다.

**Svchost.exe**

* 윈도우가 다양한 기능을 수행하는 데 사용하는 다른 개별 서비스를 호스팅 하거나 포함하는 프로세스

**lsass.exe**

* Winlogon.exe의 요청에 의해 인증과 관련된 부분을 처리하는 프로세스

**winlogon.exe**

* 사용자 로그온/로그오프를 담당하는 프로세스이다. 윈도우 시작/종료 시에 활성화되며 단축키 Ctrl+Alt+Del을 눌러도 활성화된다.

---





