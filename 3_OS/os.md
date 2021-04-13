# Operation System

### 디스크 스케줄링

* FCFS

* SSTF 

* SCAN

  * 좌우 왕복하면서 가는 길에 처리한다

  ![image](https://user-images.githubusercontent.com/75229881/110737022-fa76c300-826f-11eb-960a-27499f930912.png)

* C-SCAN

  * 한 쪽 방향으로만 이동한다

  ![image](https://user-images.githubusercontent.com/75229881/110737211-4a558a00-8270-11eb-896a-7a7f71f22823.png)

* LOOK/C-LOOK

  * 끝까지는 안간다

  ![image](https://user-images.githubusercontent.com/75229881/110737261-63f6d180-8270-11eb-8cbf-d2e8dff088c7.png)

---

### 제어장치의 구성요소
* 명령 계수기(PC) 
  * 다음에 실행할 명령의 주소기억
* 주소 레지스터(MAR)
  * 주기억장치에 선택될 주소를 기억하는 레지스터
* 내용 레지스터(MBR)
  * PC나 MAR이 지정하는 주기억장치의 내용을 임시로 기억하는 레지스터 
* 명령 레지스터(IR)
  * PC가 지정한 주소의 명령을 인출하여 명령 실행이 완료될 때 까지 명령을 보관하는 레지스터 
* 명령 해독기
  * IR에서 보내온 명령 코드를 해독
* 인덱스 레지스터(IX)
  * 명령 어드레스나 인덱스를 변경할 때 사용
* 제어신호 발생기(부호기)
  * 명령 해독기에서 보내온 신호를 명령을 실행하는데 필요한 신호로 바꾸어 각 장치에 제어신호 전송

---

### 페이징

*  프로세스의 물리 주소 공간이 연속되지 않아도 되는 메모리 관리 기법
* 물리페이지는 frame, 논리메모리는 page로 분할된다
* 예제
  * 페이지 크기는 2000byte
  * 논리주소가 2500이면 페이지번호는 1번임, 이에 해당하는 프레임번호가 3번, 오프셋은 500
  * 물리주소는 6500
* 페이징 자체는 일종의 동적 재배치

---

### RAID

* RAID 0 (스트라이핑)
  * 읽기/쓰기 n배 상향
  * 디스크 수 * Disk 용량
  * 낮은 안정성
* RAID 1 (미러링)
  * 읽기 n배 상향, 쓰기 시 성능 감소
  * 디스크 수 /2 * 용량
  * 높은 안정성
* RAID 2
  * 해밍코드
* RAID 3/4
  * 데이터 스트라이핑 및 별도의 Parity disk 사용
  * 3 - byte 단위 / 4 - block 단위
* RAID 5
  *  Block 레벨의 Striping과 Parity 사용(Parity 분산 제공)
  * 읽기 N배, 쓰기 성능이 (N-1)배 향상
* RAID 6
  *  Block 레벨의 Striping과 Double Parity 사용(Parity 분산 제공)
  * 읽기 N배, 쓰기 성능이 (N-2)배 향상

---

### 프로세스 스케줄링

**비선점**

* FCFS
* SJF
  * 실행시간이 짧은 스케줄 먼저 실행
* HRN
  * (대기시간 + 실행시간) / 실행시간으로 우선순위를 결정, 높을수록 우선순위가 높음

**선점**

* RR
  * 각 프로세스마다 동일한 실행시간 부여
* SRT
  * SJF와 비슷하나 짧은 스케줄이 들어왔을 때 선점가능
* Multi-Level Queue
  * 여러 큐를 형성하여 높은 우선순위의 큐에 있는 작업이 우선순위를 가진다.
* Multi-Level Feedback Queue
  * 각 큐에 time-quantum을 적용하여 실행시간이 길어지면 아래 큐로 보낸다.
  * 보통 밑으로 갈수록 time이 길고 마지막에는 FCFS로 처리

---

### CISC/RISC

**CISC**

* 명령어의 개수가 다양하며 길이는 가변적
* 고급언어에 대해 각각 기계어가 대응되도록 하는 것, 복잡한 구조를 가진다.
* 복잡한 컴파일러, 회로구성 복잡
* 복잡한 명령이 많기 때문에 마이크로 프로그램으로 제어한다.

**RISC**

* 명령어의 개수가 적으며 고정 길이를 가진다.
* 단순한 컴파일러, 회로구성 단순
* 단순 명령이 많기 때문에 다수의 레지스터가 필요하고 하드와이어(Hard-wired)방식으로 제어한다.

---

### 프로세스 상태전이

![process_state](https://user-images.githubusercontent.com/75229881/113966976-0ce21d80-986b-11eb-9bf5-e879ae14dc4d.png)

* 상태전이
  * Dispatch - 프로세스 스케줄러에 의해 결정된 우선순위에 따라 프로세스가 CPU를 점유하게 되는 상
  * Time out - 프로세스가 실행중이다가 제한된 시간을 다 소비하여 CPU 점유를 빼앗기는 상태
  * Block - 실행중이던 프로세스가 외부 요인에 의해서 자원을 빼앗기는 상태
  * Wake up - 프로세스가 자원을 할당받는 상태
  * Swap in - 프로세스가 주기억장치에 적재 되는 상태
  * Swap out - 프로세스가 주기억장치에서 해제 되는 상태
* Ready 상태로의 전이
  * Running에서 Time-out
  * Asleep(I/O등의 이유로 Block됨)에서 Wake-up
  * 우선순위에 의하여 선점당했을 때

---

### 캐시

* 블록
  * 주기억장치에서 word를 나누는 단위
  * 주기억장치 용량이 2<sup>n</sup> word이고 블록 사이즈가 K word라면 블록의 수는 2<sup>n</sup>/K
* 라인
  * 캐시의 크기만큼의 라인을 가짐
  * 주기억 장치가 64 word 이고 캐시가 16 word라면 4 line을 가진다.
* 태그
  * 블록 내부의 offset

<br>

**매핑방식**

![image](https://user-images.githubusercontent.com/75229881/114500782-bb1f0600-9c63-11eb-9a73-416a15fb779a.png)

* 직접사상

  * 태그 필드에서 해당 블록의 위치를 지정
  * 라인 필드에서 라인을 지정(블록크기와 동일)
  * 단어 필드(데이터)

![image](https://user-images.githubusercontent.com/75229881/114502916-79905a00-9c67-11eb-89c9-96e026cac12c.png)

* 연관사상

  * 블록으로 안나누고 태그가 하나의 Word의 주소를 가진다

![image](https://user-images.githubusercontent.com/75229881/114503120-c2e0a980-9c67-11eb-8a12-da0b01bf4837.png)

* 세트-연관 사상

  * 세트는 블록의 묶음(2-way면 2라인을 가진다)
  * (t+d) 비트가 주기억장치의 2<sup>(t+d)</sup>를 가리킨다

---





  

