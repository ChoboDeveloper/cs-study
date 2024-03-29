# 기본지식

<br>

### 바인딩

* 바인딩(Binding) 이란 프로그램의 어떤 기본 단위가 가질 수 있는 구성요소의 구체적인 값, 성격을 확정하는 것을 말한다.

* 이름, 자료형, 자료값에 각각 `num`, `int`, `123` 이라는 **구체적인 값을 할당하는 각각의 과정**을 바인딩이라고 한다.
* 함수에서도 바인딩이 일어나는데, 이때 바인딩은 어떤 코드에서 함수를 호출할 때 그 해당 함수가 위치한 메모리 주소로 연결해주는 것을 의미한다.

**동적바인딩(Dynamic Binding)**

- **실행 시간**(Runtime) 즉, 파일을 실행하는 시점에 성격이 결정된다
- 함수의 정적 바인딩은 컴파일 시간에 호출될 해당 함수의 주소가 결정되어 바인딩 된다. 즉, 실행 파일에 호출할 함수가 위치한 메모리 주소가 이미 확정 기록된 것이다.
- 일반적인 함수는 정적 바인딩이 일어난다.

**정적 바인딩(Static Binding)**

- **컴파일**(Compile) 시간에 성격이 결정된다
- 함수의 동적 바인딩은 실행파일을 만들 때 호출할 함수의 메모리 주소가 확정되지 않고 보류상태로 둔다. 이후 실제 실행 시간에 호출할 함수의 주소가 결정되기 때문에, 이 주소를 저장할 공간을 미리 확보해둔다(4byte). 실행될지 확정되지 않은 함수를 위해 저장공간을 빼둬야 하는 점 때문에 메모리 관리에 있어 비효율적일 수 있다.
- 보통 가상함수들이 동적 바인딩

---

### **정규표현식**

**POSIX**

| 메타문자 |        기능         |                             설명                             |
| :------: | :-----------------: | :----------------------------------------------------------: |
|    .     |        문자         | 1개의 문자와 일치한다. 단일행 모드에서는 [새줄 문자](https://ko.wikipedia.org/wiki/새줄_문자)를 제외한다. |
|   [ ]    |     문자 클래스     | "["과 "]" 사이의 문자 중 하나를 선택한다. "¦"를 여러 개 쓴 것과 같은 의미이다. 예를 들면 [abc]d는 ad, bd, cd를 뜻한다. 또한, "-" 기호와 함께 쓰면 범위를 지정할 수 있다. "[a-z]"는 a부터 z까지 중 하나, "[1-9]"는 1부터 9까지 중의 하나를 의미한다. |
|   [^ ]   |        부정         | 문자 클래스 안의 문자를 제외한 나머지를 선택한다. 예를 들면 [^abc]d는 ad, bd, cd는 포함하지 않고 ed, fd 등을 포함한다. [^a-z]는 알파벳 소문자로 시작하지 않는 모든 문자를 의미한다. |
|    ^     |        처음         |               문자열이나 행의 처음을 의미한다.               |
|    $     |         끝          |                문자열이나 행의 끝을 의미한다.                |
|   ( )    |       하위식        | 여러 식을 하나로 묶을 수 있다. "abc¦adc"와 "a(b¦d)c"는 같은 의미를 가진다. |
|    \n    | 일치하는 n번째 패턴 | 일치하는 패턴들 중 n번째를 선택하며, 여기에서 n은 1에서 9 중 하나가 올 수 있다. |
|    *     |      0회 이상       | 0개 이상의 문자를 포함한다. "a*b"는 "b", "ab", "aab", "aaab"를 포함한다. |
|  {m, n}  |  m회 이상 n회 이하  | "a{1,3}b"는 "ab", "aab", "aaab"를 포함하지만, "b"나 "aaaab"는 포함하지 않는다. |

**POSIX 확장**

| 메타문자 |    기능    |                             설명                             |
| :------: | :--------: | :----------------------------------------------------------: |
|    ?     | 0 또는 1회 |                "a?b"는 "b", "ab"를 포함한다.                 |
|    +     |  1회 이상  | "a+b"는 "ab", "aab", "aaab"를 포함하지만 "b"는 포함하지 않는다. |
|    ¦     |    선택    | 여러 식 중에서 하나를 선택한다. 예를 들어, "abc¦adc"는 abc와 adc 문자열을 모두 포함한다. |

---

### 포인터 변수

* 프로그래밍 언어에서 다른 변수, 혹은 그 변수의 메모리 공간주소를 가리키는 변수이다.
* 즉, 64비트 프로세서에 맞춰 컴파일하면 8바이트, 32비트 프로세서에 맞추면 4바이트의 크기를 가진다.

---

### 컴파일 순서

**C Language**

1. 전처리(Preprocessing)
   * include 라이브러리, define 치환 등
2. Compile
   * 어셈블러 코드 생성
3. Assemble
   * 목적파일(hello.o) 생성
4. Link
   * hello 실행파일 생성

**Java**

---

### 추상화

- 주어진 작업이나 객체를 속성들의 일부분을 가지고 필요한 만큼 묘사할 수 있는 방법을 지원하는 것
- 필수적인 속성만으로 주어진 것을 묘사하므로 나머지 속성들은 추상화, 은닉 또는 삭제된다.

<br>

**자료 추상화**

* 기본적 추상화
  * 컴퓨터 내부의 자료 표현을 추상화

```c
* 기억 장치의 위치 -> 변수로 추상화
int x;
float y;
* 자료의 값(2진수) -> 10진수(정수, 실수) 자료형으로 추상화
x = 5.7;
```

* 구조적 추상화
  * 관련된 자료값의 집합을 추상화한다. 배열과 레코드와 같은 구조형 자료가 전형적인 구조적 추상화의 예이다.

```python
type student = record
```

* 단위 추상화
  * 자료의 생성과 사용에 대한 정보를 한 장소에 모아두고, 자료의 세부사항에 대한 접근을 제한하는 도구
* Class, Module 등

<br>

**제어 추상화**

* 기본적 추상화
  * 몇 개의 기계 명령어를 모아 이해하기 쉬운 추상 구문으로 만든 것

```fortran
* 계산과 값의 저장을 추상화한 배정문
x := x + y
* 분기문 (Fortran의 GOTO문이나 if문 등)
IF (A.GT.B) GOTO 10
```

* 구조적 추상화

```java
// Java의 if 문
if (x > y) {
   t := x;
   x := y;
   y := t;
}
else {
   x := x + y;
   y := y + 1;
}

// Java의 반복문
i = 0;
do
   i = i + 1;
while (sentence[i] = '$');
```

---
