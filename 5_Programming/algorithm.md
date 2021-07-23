# Algorithm

<br>

### 문자열 탐색

**Naive**

* Naive 방식은 본문 처음부터 끝까지 문자 하나하나씩 패턴과 비교하여 찾는다
* O(nm), (n : 본문 길이, m : 패턴 길이)

**Rabin Karp**

* Rabin Karp 방식은 문자의 아스키코드(ASCII Code) 값을 이용한 해시(Hash)를 사용한다

**KMP**

* 접두사, 접미사 기준으로 일정부분을 건너뜀

**Boyer Moore**

---