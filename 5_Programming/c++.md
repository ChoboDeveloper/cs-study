# C++

<Br>

## Priority queue

```c++
// #include <queue>
// define 
template<
    class T,
    class Container = std::vector<T>,
    class Compare = std::less<typename Container::value_type>
> class priority_queue;

// example
priority_queue<int> q1;
priority_queue<int, vector<int>, cmp> q2;

// compare overloading, 기본값은 less<T>
struct a{
    int start;
    int end;
    int value;
};

// val의 작은값이 우선순위
struct cmp{
    bool operator()(a t, a t){
        return a.value > b.value;
    }
}
```

---

## Vector

**vector::erase()**

```c++
// define
iterator erase( iterator pos );

// example
v.erase(v.begin()+2); // v[2] 제거
v.erase(v.begin(), v.begin+2) // v[0], v[1], v[2] 제거
```



---

## String

**string::find**

```c++
//define
size_type find( const basic_string& str, size_type pos = 0 );
size_type find( CharT ch, size_type pos = 0 ) const;

//example
string s = "This is an example";
    string::size_type idx;

    idx = s.find("example");
    if(idx == string::npos)
        cout << "Can`t Found";
    else
        cout << idx << endl; // 11

// 4번부터 찾는다
idx = s.find("i", 4);
cout << idx << endl; // 5출력

// 특정 문자를 연속적으로 찾는다
string::size_type begin = 0;
while(1){
        idx = s.find("e", begin);
        if(idx == string::npos){
            cout << "No Found";
            break;
        }
        else
            cout << idx << endl;
        begin = idx+1;
    }
```

**string::erase**

```c++
//define
iterator erase(const_iterator position);

// example
string s = "This is an example";
s.erase(0, 5);
cout << s; // is an example

// 특정 문자를 다 지우고 싶을 때
// 1. remove 사용 include <algorithm>
// remove는 e를 제외한 모든 요소를 앞쪽으로 복사하고 마지막 위치의 iterator를 반환
// erase가 반환된 iterator 부터 end까지 제거
s.erase(remove(s.begin(), s.end(), "e"), s.end());
cout << s; // This an xampl

// 2. find 사용
int idx;
while(1){
    idx = s.find('e');
    cout << idx << endl;	// 11, 16, -1 출력
    if(idx != -1)
        s.erase(s.begin()+idx);
    else
        break;
}
cout << s << endl; // This is an xampl
```

**string::substring**

```c++
//define
basic_string substr( size_type pos = 0, size_type count = npos ) const;

//example
string a = "0123456789abcdefghij";
string sub1 = a.substr(10);
cout << sub1 << '\n';	// abcdefghij

string sub2 = a.substr(5, 3);
cout << sub2 << '\n';	// 567

// 특정 구분자를 제외시킨 문장
string s = "This<div>is<div>a<div>string";
int idx = 0;
int begin = 0;
string seperator = "<div>";
while(idx != -1){
    idx = s.find(seperator, begin);
    string tmp = s.substr(begin, idx - begin);
    begin = idx+seperator.size();
    cout << tmp;
}	// Thisisastring
```



---

## Stringstream

* 공백, \n을 제외한 연속적인 입력

```c++
#include <sstream>

//example
string str1 = "23 259 .326 22 a 15"; 

stringstream ss(str1);
string k; 
while(ss >> k) cout << k << endl;
// kk 259 abc 22 def qwer

ss.clear();
ss.str(str1);
string s[4];
ss >> s[0] >> k >> s[1] >> k >> s[2] >> s[3];
for(auto i : s) cout << i << " "; 
cout << k;
//kk abc def qwer 22


```



---

### 연산자 우선순위

| 연산자                                                | 연산 유형    |
| :---------------------------------------------------- | :----------- |
| `[` `]` `(` `)` `.` `->` `++` `--` (후위)             |              |
| **`sizeof`** `&` `*` `+` `-` `~` `!` `++` `--` (전위) | 단항         |
| *형식 캐스팅*                                         | 단항         |
| `*` `/` `%`                                           | 곱셈, 나눗셈 |
| `+` `-`                                               | 덧셈, 뺄셈   |
| `<<` `>>`                                             | 비트 시프트  |
| `<` `>` `<=` `>=`                                     | 비교         |
| `==` `!=`                                             | 같음, 다름   |
| `&`                                                   | 비트 AND     |
| `^`                                                   | 비트 XOR     |
| `|`                                                   | 비트 OR      |
| `&&`                                                  | 논리 AND     |
| `||`                                                  | 논리 OR      |
| `? :`                                                 | 조건식       |

1. 괄호
2. 단항연산자
3. 연산
4. 시프트
5. 비교
6. 비트연산자
7. 논리
8. 조건식

---

### Union

*  Union(공용체)의 크기는 공용체 멤버 변수 중 가장 큰 크기의 값을 하나 할당하고 모든 멤버가 그 메모리를 공유하게 된다.
* 예를 들어 공용체 멤버 변수로 long, int, char를 둘 씩 선언할 경우 그 중에서 가장 큰 long의 8바이트를 멤버 변수 전체가 공유해 총 크기가 8Byte가 된다.

---

### 심볼 테이블

* Symbol table은 다음과 같은 정보를 저장하기 위해 컴파일러에서 생성하는 자료구조

  - Variable name
  - Function name
  - Objects, Classes, Interfaces

* 이를 통해 name(label)을 체계적으로 관리한다. 또한, 선언 여부, type checking, scope checking(Global, Local) 등을 할 수 있다.

* 예제

  * 아래 예시 코드를 이용하여 컴파일러는 Fig1과 같은 계층구조의 symbol table을 생성한다. 어떤 함수에서 symbol table을 접근하면, 우선 현재 scope의 symbol table을 뒤지고, 없으면 parent로 올라간다. (until global symbol table)

    ```
    int value=10;
    
    void pro_one()
       {
       int one_1;
       int one_2;
       
          {              \
          int one_3;      |_  inner scope 1 
          int one_4;      | 
          }              /
          
       int one_5; 
       
          {              \   
          int one_6;      |_  inner scope 2
          int one_7;      |
          }              /
       }
       
    void pro_two()
       {
       int two_1;
       int two_2;
       
          {              \
          int two_3;      |_  inner scope 3
          int two_4;      |
          }              /
          
       int two_5;
       }
    ```

    ![image](https://user-images.githubusercontent.com/75229881/163799314-3325b01a-1c32-4557-8d13-0a3b6005d5f7.png)

    

---
