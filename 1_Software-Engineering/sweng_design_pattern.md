# 디자인 패턴



### 분류하기



팩토리 메서드, 추상팩토리, 프록시, 프로토타입, 싱글톤, 어댑터, 컴포지트,
템플릿 메소드, 플라이웨이트, 스트레지티, 옵저버, 데코레이터, 퍼사드, 커맨드


---



### 문제풀기



* 다음 내용이 설명하는 디자인 패턴은?  

```
* 객체를 생성하기 위한 인터페이스를 정의하여 어떤 클래스가 인스턴스화 될 것인지는 서브클래스가 결정하도록 하는 것
* Virtual-Constructor 패턴이라고도 함
```



---



* 다음과 같은 구조를 가진 디자인 패턴은?

![adapter](https://user-images.githubusercontent.com/75229881/109116194-7c042680-7783-11eb-8b2c-a3d387bc66fe.PNG)

---



* 다음 내용이 설명하는 디자인 패턴은?


동일 계열의 알고리즘군을 정의하고, 각 알고리즘을 캡슐화하며, 이들을 상호교환이 가능하도록 만듭니다. 
알고리즘을 사용하는 클라이언트와 상관없이 독립적으로 알고리즘을 다양하게 변경할 수 있게 합니다.



---

* 다음 내용이 설명하는 디자인 패턴은?

```python
from abc import ABCMeta, abstractmethod

    class Order(metaclass=ABCMeta):
    	@abstractmethod
        def execute(self):
            pass

    class BuyStockOrder(Order):
        def __init__(self, stock):
        	self.stock = stock
        def execute(self):
        	self.stock.buy()
    
    class SellStockOrder(Order):
        def __init__(self, stock):
        	self.stock = stock
        def execute(self):
        	self.stock.sell()
    
    class StockTrade:
        def buy(self):
        	print(“You will buy stocks”)
        def sell(self):
        	print(“You will sell stocks”)
    
    class Agent:
        def __init__(self):
        	self.__orderQueue = []
        def placeOrder(self, order):
        	self.__orderQueue.append(order)
    		order.execute()
    
if __name__ == ‘__main__’:
    #Client
    stock = StockTrade()
    buyStock = BuyStockOrder(stock)
    sellStock = SellStockOrder(stock)
    #Invoker
    agent = Agent()
    agent.placeOrder(buyStock)
    agent.placeOrder(sellStock)
```



---

* 차량 네비게이션 SW에서 GPS를 수신하는 경우와 수신하지 못하는 경우에 따라 차량의 위치를 구하는 다른 알고리즘을 선택하고자 할 때 적합한 디자인 패턴은?

---

