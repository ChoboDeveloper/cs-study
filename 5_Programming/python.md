# Python

<br>

### 클래스

* 상속 시 class 클래스명(상속받을 클래스명):
* 오버로딩은 지원안함

```python
class Person: 
    def __init__(self, name, age, gender): 
        self.Name = name 
        self.Age = age 
        self.Gender = gender 
        
    def aboutMe(self): 
        print("저의 이름은 " + self.Name + "이구요, 제 나이는 " + self.Age + "살 입니다.")


class Employee(Person): 
    def __init__(self, name, age, gender, salary, hiredate): 
        Person.__init__(self, name, age, gender) 
        self.Salary = salary self.Hiredate = hiredate 
        
    def doWork(self): print("열심히 일을 합니다.") 

    def aboutMe(self): 
        Person.aboutMe(self) 
        print("제 급여는 " + self.Salary + "원 이구요, 제 입사일은 " + self.Hiredate + " 입니다.")
        
>>> objectEmployee = Employee("김철수", "18", "남", "5000000", "2013년 10월 28일") 
>>> objectEmployee.doWork() 
열심히 일을 합니다. 
>>> objectEmployee.aboutMe() 
저의 이름은 김철수이구요, 제 나이는 18살 입니다. 제 급여는 5000000원 이구요, 제 입사일은 2013년 10월 28일 입니다.

```



---

### 리스트

```python
>>> a = [1, 2, 3, 4, 5]
>>> b = a[:2]
>>> c = a[2:]
>>> b
[1, 2]
>>> c
[3, 4, 5]
```

```python
kospi = ['삼성전자', 'SK하이닉스', '현대차']

kospi.insert(0, 'Google')
print(kospi)	# ['Google', '삼성전자', 'SK하이닉스', '현대차']

kospi.append('apple')
print(kospi)	# ['Google', '삼성전자', 'SK하이닉스', '현대차', 'apple']

kospi.pop()
print(kospi)	# ['Google', '삼성전자', 'SK하이닉스', '현대차']

kospi.remove('Google')
print(kospi)	# ['삼성전자', 'SK하이닉스', '현대차']

del kospi[-1]
print(kospi)	# ['삼성전자', 'SK하이닉스']
```



---

### 딕셔너리

```python
>>> price = {'Daum KAKAO': 80000, 'naver':800000, 'daeshin':30000}
>>> price['google']=150000

>>> print(price)
{'Daum KAKAO': 80000, 'naver': 800000, 'daeshin': 30000, 'google': 150000}

>>> del price['naver']
>>> print(price)
{'Daum KAKAO': 80000, 'daeshin': 30000, 'google': 150000}
```



---

