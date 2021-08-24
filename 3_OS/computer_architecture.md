# 컴퓨터 구조

<br>

### 순차회로

* 외부로부터의 입력과 현재 상태에 따라 출력이 결정되는 회로
* 기억소자가 존재

* 플립플롭, 카운터, 레지스터, RAM, CPU

**플립플롭**

![image](https://user-images.githubusercontent.com/75229881/115541552-37f05680-a2da-11eb-9a76-29164afb6a66.png)

---

### 조합회로

* 논리 게이트로 구성되며 기억회로는 가지고 있지 않기 때문에 이전 입력과 관계없이 현재의 입력 조합으로부터 출력 값이 결정된다

* 반가산기, 전가산기, 디코더, 인코더, 멀티플렉서, 디멀티플렉서

**반가산기**

* A = B = 1, CARRY = 1

![image](https://user-images.githubusercontent.com/75229881/115542007-c369e780-a2da-11eb-8700-7d8ba57a0d25.png)

**반감산기**

![image](https://user-images.githubusercontent.com/75229881/115542053-d2e93080-a2da-11eb-92c2-474516c3cfd5.png)

**인코더**

* 2<sup>n</sup> 개의 입력과 n개의 출력

**디코더**

* n개의 입력과 2<sup>n</sup> 개의 출력

**멀티플렉서**

* 여러 입력 신호 중 하나를 선택해서 출력

**디멀티플렉서**

* 하나의 입력 신호를 여러개의 출력 신호중 하나로 출력

---

### Flynn의 분류

* SISD
  * 단일 명령어 / 단일 데이터 흐름
  * 파이프라이닝과 슈퍼스칼라(파이프라인x2)를 이용하여 병렬처리
* SIMD
  * 단일 명령어 / 다중 데이터 흐름
  * 배열 프로세서
  * CUDA처럼 동시에 배열을 한번에 찍어내는 연산
* MISD
  * 실제 구현X
  * 다중 명령어 / 단일 데이터 흐름
* MIMD
  * 다중 처리기
  * 다중 명령어 / 다중 데이터 흐름

---

### 병렬처리 종류

* 파이프라인
  * Fetch, Decode, Execute, Write-back 등의 각기 다른 작업의 명령을 한 클럭에 동시에 실행
  * 파이프라이닝은 다수의 브런치나 서브루틴 콜이 발생하면 효율이 떨어지기 때문에 최신 아키텍처는 분기예측 기법을 통해 이런 문제를 회피
    * 분기의 결과를 예측하여 기다리지 않고 파이프라인에 넣음, 틀리면 명령어 삭제
* 멀티 프로그래밍
  * RAM에 여러 프로세스를 올려서 사용
* 벡터 프로세싱
  *  SIMD를 의미
* 멀티 프로세싱
  * 다중 처리기를 의미

---

### 다중 처리기(Multi-Processor)

* Master/Slave 처리기
  * Master : 입출력, 연산, OS
  * Slave : 연산
* 분리 실행 처리기
  * 각 프로세서가 독자적인 OS 보유
  * 할당된 작업은 해당 프로세서가 모두 처리해야 되기 때문에 한 프로세서에 일이 밀려도 다른 프로세서는 유휴 상태가 될 수 있다.
* 대칭적 처리기
  * 분리 실행 처리기 구조의 문제점을 보완한 것으로, 여러 프로세서들이 완전한 기능을 갖춘 하나의 운영체제를 공유하여 수행하는 구조이다.
  * 프로세서 간의 통신은 공유 메모리를 통해 이루어진다.

**프로세서 결합도**

* 강결합 시스템
  * 하나의 OS가 처리
  * 여러 CPU와 하나의 공유 메모리 구조
  * 복잡하고 결합력이 강함, 
  * 프로세서 추가해도 성능향상이 없음
* 약결합 시스템
  * 분산 처리기, 여러 OS가 처리
  * 독자적인 메모리를 가짐
  * 프로세서간 통신은 메시지 혹은 원격 프로시저를 호출

---

### 다중 처리기 연결방식

* 하이퍼큐브

  ![image](https://user-images.githubusercontent.com/75229881/116369782-b8680780-a844-11eb-9f83-e1622d0230e1.png)

  * 분산기억장치 시스템
  * 연결점이 n이면 2<sup>n</sup>개의 CPU 존재
  * 경제적이고 확장성이 좋음

* 시분할 및 공유버스

  ![image](https://user-images.githubusercontent.com/75229881/116370002-f06f4a80-a844-11eb-906b-19f3ebf18605.png)

  * 프로세서, 주변장치, 주기억장치 등을 단일 버스로 연결
  * 장치 추가가 용이하며 한 시점에 한 번의 전송만이 가능

* 크로스바 교환 행렬

  ![image](https://user-images.githubusercontent.com/75229881/116370134-0ed54600-a845-11eb-820d-c6f6d55577c5.png)

  * 버스의 수를 메모리의 수 만큼 증가
  * 기억장치의 동시참조 가능

* 다중 포트 기억장치

  

  <img src = "https://user-images.githubusercontent.com/75229881/116370297-362c1300-a845-11eb-9638-3f1a9d903f39.png" width="50%">

  * 시분할 및 공유 버스 기법 + 크로스바 교환 행렬
  * 다양한 연결이 가능하지만 전송시간이 느리다.

---

### SMT(Simultaneous Multi-Threading)

* 하이퍼스레딩
* 하나의 코어에 여러 스레드를 올려서 사용하는 기법
* 동시에 처리할 수 있는 명령들을 1개의 코어가 동시에 작업한다
* sw적으로 코어가 두개처럼 보인다

---

### 파이프라이닝 해저드

* 구조 해저드
  * 명령어가 사용하는 자원의 충돌이 발생하지만 구조적으로 하드웨어가 지원해 줄 수 있는 자원이 없는 경우 발생
  * 부족한 자원의 추가로 해결
* 데이터 해저드
  * 앞의 명령어에서 완전히 write를 끝내기 전에 다음 명령어가 read 하는 것처럼 명령어 사이에 종속성이 존재할 경우
  * 데이터 포워딩을 통해 해결, 별도의 하드웨어를 추가 하여 정상적으로는 얻을 수 없는 값을 내부 자원으로부터 일찍 받아오는 것
* 제어 해저드
  * 앞서 분기 명령어에 의해 필요없는 명령어가 실행되는 경우
  * 분기 예측을 통해 해결

---

### 마이크로 오퍼레이션

```
Instruction Cycle Code,
00 : Fetch Cycle 
01 : Indirect Cycle 
10 : Execute Cycle 
11 : Interrupt Cycle 
```

* Fetch
  * t1 : MAR <- PC
    * 명령어가 저장된 주소를 MAR로 전송
    * **주소버스**를 통해 주소를 전달받고 **제어버스**를 통해 Read 명령을 실행
  * t2 : MBR <- M[MAR], PC <- PC+1
    * 메모리에서 명령어를 인출하여 MBR로 전송
    * **데이터버스**를 통해 메모리에 저장된 데이터를 반환
  * t3 : IR <- MBR
    * 명령어 디코딩을 위해 MBR의 데이터를 IR로 전송 및 PC는 다음 주소를 가리킴
    * 이후 IR에서 명령어 디코딩 및 실행하여 **제어버스**를 통해 제어신호를 전달
* Indirect
  * t1 : MAR <- IR[Address]
  * t2 : MBR <- M[MAR]
  * t3 : IR[Address] <- MBR[Address]
* Execute
  * ADD R, X (레지스터 R에 X의 내용을 더하라)
  * t1 : MAR <- IR[Address]
  * t2 : MBR <- M[MAR]
  * t3 : R <- R + MBR
* Interrupt
  * t1 : MBR <- PC
  * t2 : MAR <- Save Address, PC <- Routine Address
  * t3 : M[MAR] <- MBR

---

### 버스

```
버스대역폭 = 버스의 클럭 주파수 X 데이터 버스의 폭
ex) 
버스의 클록 주파수가 100Mhz이고 데이터 버스의 폭이 32Bit(4Byte)
-> 400 MByte/sec
```

**시스템버스**

* 주소버스
* 제어버스
* 데이터버스

**I/O 버스**

---

### Instruction Set

**Instruction**

* Opcode + Operand 구성
  * **3 + 6 = 9** 라는 연산이 있을 때 '+' 이 **Opcode** 이고 3, 6 이 **Operand**

**Number of Address**

* 3 주소
  * Operand1, Operand2, Operand3(Result) 로 구성
  * A = B + C
* 2 주소
  * A = A + B
* 1 주소
  * AC <- A
* 0 주소
  * 주소가 필요없는 명령, 스택을 활용한다.
  * PUSH A

**Addressing Mode**

>Instruction Fetch 되어 있기 때문에 명령어는 CPU에 있다. 
>
>그리고 대부분의 데이터는 memory에 있다

**메모리 접근**

* Immediate Addressing
  * 데이터가 Memory에 있는게 아니라 명령어 안에 있는 것
    * ADD 5 (Operand안에 5라는 **데이터**가 있음)
* Direct Addressing
  * Operand에 Memory의 주소가 있음
  * EA(Effective address) = A
* Indirect Addressing
  * 메모리에 데이터의 포인터
  * EA = (A)

**레지스터 접근**

* Register Addressing
  * 메모리 참조 필요없음 / 주소 제한적(레지스터 몇개 없음)
  * EA = R
* Register Indirect Addressing
  * 레지스터에 데이터의 포인터 / 메모리 참조 
  * EA = (R)

**Displacement Addressing(변위주소)**

> EA = A + (R)의 형태

* **Relative addressing**
  * 변위정보는 PC 값
  * 프로그램 카운터는 알아서 increment를 해주는 특징이 있다. 32 비트면 4만큼 64비트면 8만큼 increment한다. 
  * 알아서 increment를 시켜주니 Relative Addressing이라고 한다.
  * EA = A + (PC)
* **Base-Register addressing** 
  * 변위정보는 A
  * EA = A + (R)
* **Indexing Addressing** 
  * 변위정보는 레지스터
  * EA = A + (R)

---