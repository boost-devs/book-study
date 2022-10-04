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

## 4장. 팩토리 패턴

## 5장. 싱글턴 패턴

## 6장. 커맨드 패턴

## 7장. 어댑터 패턴과 퍼사드 패턴

## 8장. 템플릿 메소드 패턴

## 9장. 반복자 패턴과 컴포지트 패턴

## 10장. 상태 패턴

## 11장. 프록시 패턴

## 12장. 복합 패턴

## 13장. 실전 디자인 패턴

## 14장. 기타 패턴

## References

- [Python ABC(Abstract Base Class) 추상화 클래스 | ㅍㅍㅋㄷ](https://bluese05.tistory.com/61)
