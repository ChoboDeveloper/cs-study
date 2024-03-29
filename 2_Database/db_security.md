# 데이터베이스 보안

<br>

**정의**

* 데이터베이스 보안을 강화하면 공격자가 내부 네트워크에 들어와서 데이터베이스가 유출되었다 하더라도 **핵심 자산인 데이터베이스는 암호화 되어있기 때문에 볼 수 없다.**
* 사용자 인증, 접근통제, 데이터베이스 무결성 보장, 감사, 비밀 데이터의 보호 및 관리 등이 포함된다.

<br>

**데이터베이스 보안 위협**

- 집성(Aggregation) 공격 : 낮은 보안등급의 정보조각을 조합하여 높은 등급의 정보를 알아내는 것.
  - ex) 공개된 지사별 영업실적으로 1등급인 총 매출액을 유추해낼 수 있다.
- **추론(Inference) 공격** : 보안으로 분류되지 않은 정보에 접근한 후 기밀정보를 유추하는 것
- **데이터 디들링(Data Diddling)** : 처리할 자료를 다른 자료와 바꿔서 처리하는 공격. 즉 입력값이나 출력값을 부정한 의도로 수정하여 잘못된 결과가 나오도록 유도하는 방법

<br>

**데이터베이스 보안 요구사항**

- 부적절한 접근방지
  - 모든 사용자의 접근요청을 DBMS가 검사하고 승인된 사용자만 접근토록 해야 함
- 추론방지
  - 일반적 데이터로부터 비밀정보를 획득하는 추론이 불가능하도록 해야 함
- 운영적 무결성 보장
  - 트랜잭션의 병행처리 동안에 데이터에 대한 논리적인 일관성을 보장해야 함
    - 로킹(Locking) 기법 등과 같은 병행 수행 제어 기법 등이 사용되어야 함
    - 로킹기법 : 고유 가능한 데이터에 대한 접근을 상호배타적으로 통제하는 병행수행제어기법으로 데이터의 논리적 일관성 보장
- 의미적 무결성 보장
  - 데이터베이스는 데이터에 대한 허용값을 통제함으로써 변경 데이터의 논리적 일관성을 보장해야 함
- 감사기능
  - 데이터베이스에 대한 모든 접근에 대한 감사기록을 생성해야 함
- 사용자 인증
  - DBMS는 운영체제의 사용자 인증과 별개로 엄격한 인증이 요구됨

<br>

**데이터베이스 보안 통제**

- 접근 통제
  - 인증된 사용자에게 허가된 범위 내에서 시스템 내부의 정보에 대한 접근을 허용하는 기술적인 방법
  - 사용자가 DB에 접근할 때는 접근 권한이 있는지 검사하여 허용 여부를 결정
- 추론 통제
  - 간접적으로 노출된 데이터를 통해 다른 데이터를 추론하여 다른 데이터가 공개되는 것을 방지
  - 추론 방지를 위한 방법
    - 허용 가능한 질의를 제한
    - 질의의 응답으로 제공되는 데이터를 한정
    - 데이터를 숫자의 경우 반올림하거나 일관성이 없는 결과 노이즈를 포함
- 흐름 통제
  - 접근이 가능한 객체들 간의 정보의 흐름을 조정
    - 정보의 흐름: A값이 B에 기록이 되었다면 이를 'A에서 B로 흐름이 발생했다'고 함
  - 보안 등급이 높은 객체에서 낮은 객체로의 정보흐름을 제어

---

