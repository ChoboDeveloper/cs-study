# C++_STL

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

---

