## 1장. 디자인 패턴 소개와 전략 패턴

## 2장. 옵저버 패턴

![observer-uml](./images/observer.png)

**한 객체의 상태가 바뀌면 그 객체에 의존하는 다른 객체에게 연락이 가고 자동으로 내용이 갱신되는 방식**으로 일대다(one-to-many) 의존성을 정의한다. (= 일종의 브로드캐스팅 방식)

- 상태를 가지고 있는 객체를 `Subject`, 이 상태를 모니터랑하는 객체를 `Observer`라고 한다.
- 객체의 상태 변화에 관심 있는 Observer가 몇 개인지와 상관 없이 알림이 가도록 구현해야 한다.
- Subject, Observer를 분리 구현하기 때문에, Subject와 Observer가 각각 변경사항이 생겨도 서로에게 영향을 미치지 않는다. (= 느슨한 결합)
  - Observer를 언제든지 새로 추가하거나 제거할 수 있다.
  - 새로운 형식의 Observer를 추가할 수 있다.
- 최신 상태값을 가져오는 방법은 2가지이다.
  - **방법 1**: Subject가 전체 Observer에게 Push하는 방법 (= Subject가 상태를 인자로 넘겨 Observer에서 변경)
  - **방법 2**: Observer가 Subject로부터 상태를 Pull하는 방법 (= update 메서드 구현 시 getter 함수로 Subject의 상태를 가져와 변경)

### Subject

```python
from abc import ABCMeta, abstractmethod


class Subject:
  __metaclass__ = ABCMeta

  @abstractmethod
  def registerObserver(self, observer):
    pass

  @abstractmethod
  def removeObserver(self, observer):
    pass

  @abstractmethod
  def notifyObservers():
    pass


class WeatherData(Subject):

  def __init__(self):
    self._observers = []
    self._temperature = None
    self._humidity = None
    self._pressure = None

  def registerObserver(self, observer):
    self._observers.append(observer)

  def removeObserver(self, obeserver):
    try:
      self._observers.remove(observer)
    except:
      pass

  def notifyObservers(self):
    for observer in self._observers:
      observer.update(self._temperature, self._humidity, self._pressure)

  def measurementChanged(self):
    self.notifyObservers()

  def setMeasurements(self, temperature, humidity, pressure):
    self._temperature = temperature
    self._humidity = humidity
    self._pressure = pressure

    self.measurementChanged()
```

### Observer

```python
class Observer:
    __metaclass__ = ABCMeta

    @abstractmethod
    def update(self, temp, humidity, pressure):
        pass


class DisplayElement:
    __metaclass__ = ABCMeta

    @abstractmethod
    def display(self):
        pass


class CurrentConditionsDisplay(Observer, DisplayElement):

    def __init__(self, weather_data):
        self._temperature = None
        self._humidity = None
        self._weather_data = weather_data

        weather_data.registerObserver(self)

    def update(self, temperature, humidity, pressure):
        self._temperature = temperature
        self._humidity = humidity
        self.display()

    def display(self):
        print(f"현재 조건: 온도 {self._temperature} °F / 습도 {self._humidity}");
```

## 3장. 데코레이터 패턴

### 디자인 원칙: OCP(Open-Closed Principle)

> 클래스는 확장에는 열려 있어야 하지만 변경에는 닫혀 있어야 한다.

https://blog.itcode.dev/posts/2021/08/14/open-closed-principle

### 데코러이터 패턴

![decorator-uml](./images/decorator.png)

**객체에 추가 요소를 동적으로 더할 수 있는 방식**으로 서브클래스를 만들 때보다 훨씬 유연하게 기능을 확장할 수 있다.

- 데코레이터 슈퍼클래스는 장식할 객체의 슈퍼클래스와 같다.
- 한 객체에 여러 개의 데코레이터를 감쌀 수 있다.
- 데코레이터는 장식할 객체에게 어떤 행동을 위임하는 일 말고도 추가 작업을 수행할 수 있다.
- 데코레이터에서 "상속"을 사용하는 이유는 구성 요소와의 형식믈 맞추기 위함이다.
  - 구성 요소가 추상 클래스라면 똑같이 추상 클래스를, 인터페이스라면 인터페이스로 구현한다.
- 새로운 기능을 더하고 구성 요소는 데코레이터의 존재를 알 수 없다는 점에서 매우 확장성이 높지만, 다음과 같은 단점이 있다.
  - 자잘한 클래스가 많이 추가되는 경우를 볼 수 있다.
  - 구성 요소를 초기화하는 데 필요한 코드가 훨씬 복잡해진다.

#### Component

```python
from abc import ABCMeta, abstractmethod


class Beverage:
  __metaclass__ = ABCMeta

  def __init__(self):
    self._description = "Unknown Beverage"

  def get_description(self):
    return self._description

  @abstractmethod
  def cost(self):
    pass


class Espresso(Beverage):

    def __init__(self):
      self._description = "Espresso"

    def cost(self):
      return 1.99
```

#### Decorator

```python
class CondimentDecorator(Beverage):
  __metaclass__ = ABCMeta

  @abstractmethod
  def get_description():
    pass

class Mocha(CondimentDecorator):

  def __init__(self, beverage):
    self._beverage = beverage

  def get_description(self):
    return self._beverage.get_description() + ", Mocha"

  def cost(self):
    return .20 + self._beverage.cost()
```

#### 사용 예시

```python
if __name__ == "__main__":
    beverage = Espresso()
    print(beverage.get_description() + " $" + str(beverage.cost()))	# Espresso $1.99

    beverage2 = Espresso()
    beverage2 = Mocha(beverage2)
    beverage2 = Mocha(beverage2)
    print(beverage2.get_description() + " $" + str(beverage2.cost()))	# Espresso, Mocha, Mocha $2.39
```

## 4장. 팩토리 패턴

### 의존성 역전 원칙

- https://blog.itcode.dev/posts/2021/08/17/dependency-inversion-principle
- https://blog.hexabrain.net/395

### 팩토리 패턴

- https://stackoverflow.com/questions/5739611/what-are-the-differences-between-abstract-factory-and-factory-design-patterns

## 5장. 싱글턴 패턴

## 6장. 커맨드 패턴

## 7장. 어댑터 패턴과 퍼사드 패턴

## 8장. 템플릿 메소드 패턴

- 후크 메서드: "사용해도 되고 안해도 되고, 사용한다면 수정해도 되고"
  - 필수로 사용해야 하는 메서드라면 추상 메서드로 정의, 선택적으로 사용해야 하는 메서드라면 후크 메서드로 정의\
- Comparable(자기 자신과 매개변수 객체 비교) vs Comparator(두 매개변수 비교) (https://st-lab.tistory.com/243)
- 탬플릿 메서드 패턴: "여러 메서드로 구성된 메서드이고 그 메서드 중 추상메서드가 있어서 이걸 구현하는 패턴"(?)
- 팩토리 메서드 패턴도 템플릿 메서드 패턴이다..? (https://refactoring.guru/ko/design-patterns/factory-method)
  - 인스턴스를 생성하는 메서드가 추상메서드이고, 템플릿 메서드가 별도로 있음
- 템플릿 메서드(상속, 메서드, 알고리즘 개요) vs 전략(구성, 클래스, 알고리즘군)


## 9장. 반복자 패턴과 컴포지트 패턴

## 10장. 상태 패턴

- 상태 패턴은 "상태"와 "상태 전이"라는 개념이 들어간 전략 패턴이다.
  - 전략 패턴: https://refactoring.guru/ko/design-patterns/strategy
  - 상태 패턴: https://refactoring.guru/ko/design-patterns/state
- 왜 다른 상태 클래스에서 다른 상태로 전이할 때 컨텍스트 객체에서 게터 메서드를 호출해서 가져오는지? 그냥 가져오면 안 되나? : getter, setter

```
ballMachine.setState(ballMachine.getAState())
ballMachine.setState(ballMachine.AState)

class ballMachin:
  State AState;
  ...
  
  public getAState():
    return this.AState
```

## 11장. 프록시 패턴

## 12장. 복합 패턴

## 13장. 실전 디자인 패턴

## 14장. 기타 패턴

## References

- [Python ABC(Abstract Base Class) 추상화 클래스 | ㅍㅍㅋㄷ](https://bluese05.tistory.com/61)
