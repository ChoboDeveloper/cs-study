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

