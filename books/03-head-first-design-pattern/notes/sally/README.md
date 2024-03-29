## 1장. 디자인 패턴 소개와 전략 패턴

생각보다 더 쉽게 잘 쓰여진 책이라는 것을 깨달았다.  
오리 시뮬레이션 게임과 같은 상황을 모두가 한번쯤은 경험/상상해보지 않았을까?  
내용 중, 나도 Joe 처럼 fly 메소드 추가하면 당연히 해결될 것이라 생각하며 글을 읽었는데, 생각치도 못한 '고무오리가 날아다니는 사건'이 발생했다.  
내가 이 책 속의 주인공이라면 과연 어떤 방법을 사용할지, 다른 방안은 무엇이 있는지 생각하면서 읽으니까 더욱 몰입이 되는 것 같다.  

슈퍼 클래스를 상속받기에는 상황이 너무 다양하고, 다른 인터페이스를 상속받아서 하위 클래스 내에서 구현하자니 코드 재활용이 안된다.  
이러한 상황이 트레이드오프라고 생각했었는데, 간단한(?) 패턴으로 이 문제를 해결할 수 있다니 패턴을 배우면 참 유용하게 쓸 수 있을 것 같다는 생각이 들었다.  
객체의 모체가 되는 클래스에서 행동(바뀌는 부분)을 분리한 후, 따로 구현하여 이 행동을 가져와서 사용하는 방식!  
이 방식을 사용하면 코드도 재활용할수도 있고, 동적으로 행동을 지정할수도 있고, 새로운 오리가 나와도 유연하게 대처할 수 있다.  
내가 보기엔 정말 완벽한 방식인 것 같은데, 책에서는 이보다도 더 좋은 방식이 있다는 것을 넌지시 알려주고 있다. 더 좋은 방법은 과연 무엇일까...  

사실, 누군가에게 이 방식을 설명하는 것은 어려운 일이다.  
그래서 이 책의 마지막 부근의 내용 중, 패턴을 알면 다른 동료들과 의사소통할 때 편리하게 구현 방식을 정할 수 있다고 한다.  
야구선수들이 서로 사인을 맞추듯, 개발자들도 사인을 맞추는 것 같다. `'전략패턴'을 사용하자!`라고 하듯이!


## 2장. 옵저버 패턴

옵저버 패턴은 어떤 이벤트가 발생한 것을 여러 객체가 주시하거나 필요로 할 때 사용할 수 있을 것 같다.  

오늘 내용은 그렇게 어렵지 않았다. 책이 쉽게 설명해줘서 그런 것 같다.
신문사와 구독자로 생각하고 읽으니, 풀/푸쉬에 대한 것도 정리가 잘 됐다.
내가 받고싶을 때만 받는 것은 풀, 내 의지와는 상관없이 알람이 오는 것이 푸쉬!
푸쉬 방법의 경우에는 옵저버가 많아질 때, 주제(subject)의 부하가 심할 것 같다는 생각이 들었는데, 마침 2장 뒷 부분에 손쉽게 풀로 변경하는 방법에 대해 나왔다.
update를 호출하는 주체가 누구냐에 따라 풀/푸쉬가 되는 걸까? 뭔가 이상하다고 생각이 들었지만, 한번 더 읽어봐야 알 것 같다.  

느슨한 결합이 확장성에 도움이 된다는 사실도 기억해두어야겠다. 친절한(?) 프로그램을 짜겠다고 결합을 든든하게 만들어두면, 확장성에 문제가 생길 수 있겠다는 것을 깨달았다. (여러 자잘한 기능들을 만들어주고 싶은 마음...!) 필요한 것만 제공하기! 서로가 서로에 대한 최소한의 정보만을 공유하도록 만들자.

대학교 때, 자바 스윙을 사용하는 프로젝트를 한 적이 있다.
내부 구조에 대해서는 이해하지 못하고 단순히 이벤트가 발생하면, 액션리스너를 통해서 그 정보를 받아온다는 사실만 알고서도 프로그램을 짤 수 있었다.
이렇듯, 그 내부 구조를 몰라도 잘 작동하도록 만들어놓으면, 다른 개발자들도 유용하게 이를 가져다 쓸 수 있다는 사실을 이 책을 읽으며 다시 한번 상기했고, 나도 이렇게 '잘 짜여진' 프로그램을 만들어서 배포해보고 싶어졌다.

## 3장. 데코레이터 패턴

데코레이터 패턴은 상속을 사용하여, 함수처럼 기존 구조를 불러내는 것 같다.

데코레이터 패턴은 내가 들어본 패턴 중에 하나라서, 엄청나게 특별한 패턴일 줄 알았는데, 생각보다 쉬워서 "내가 이해한게 맞나?"하며 다시 읽어봤다.
설명을 제대로 이해한 것인지는 의문스럽지만, 이해한 바에 의하면, "재귀함수처럼 다시 자신을 불러내면서도 추가 작업을 할 수 있다."로 해석했다.

내가 책을 읽고 생각해본 데코레이터 패턴의 장점을 적어보자면,
- 구조를 계층적으로 쌓을 수 있다는 것
- 컴파일 시와 무관하게 동적으로 계속해서, 마음대로 쌓을 수 있다는 것
- 내가 휘핑크림이라면 모카의 가격을 몰라도 되고, 내가 모카라면 에스프레소의 가격을 몰라도 가져와서 사용할 수 있다는 점
- 여러 객체에게 반영될 수 있는 특징을 여러번 선언하거나 수정하지 않아도 된다.

"디자인 원칙: 클래스는 확장에는 열려 있어야 하지만 변경에는 닫혀 있어야 한다."라는 원칙을 배웠다.
이 디자인 원칙을 생각하면서 보니까, 확실히 쉬우면서도 강력한 패턴인 것 같다는 생각이 들었다.


## 4장. 팩토리 패턴

## 5장. 싱글턴 패턴

인스턴스를 편리하게 여럿 만들기 위해 클래스를 사용해본 적은 있으나, 단 하나의 인스턴스를 만들기 위해 클래스를 짜는 방법에 대해 공부한 것은 처음이다.  
하나의 인스턴스를 만드는 것을 넘어, 여러개의 인스턴스가 생성되는 것을 막는 방법에 나와있었는데, 지금까지 읽었던 내용 중에 가장 흥미롭게 읽었다.  
생성자를 private로 만들고, 인스턴스를 리턴하는 정적 메소드를 만들어두는 방법이 인상깊었다.  
또한, 멀티스레드 환경에서 동기화 문제를 해결하는 방법 3가지도 배웠다.  
동기화 키워드를 사용하여 메소드 자체를 동기화하는 방법, 인스턴스를 처음부터 생성해두는 방법, DCL을 사용하는 방법.  
특히, 여기서는 두번이나 lock을 check하는 이유에 대해 자세히 나와있지 않았는데, 이는 두 스레드가 동시에 인스턴스가 없다고 판단한 경우에 한해서 먼저 들어온 스레드는 두번째 조건문에 걸려서 실행하게 되고, 다음 스레드는 두번째 조건문을 확인하고 실행하지 않기 위함이다...(?)   

## 6장. 커맨드 패턴

- [커맨드 패턴 설명](https://victorydntmd.tistory.com/295)
- 241 page 다이어그램이 이해하는 데에 도움이 되었다!

## 7장. 어댑터 패턴과 퍼사드 패턴

- 어댑터 패턴: 특정 클래스 인터페이스를 클라이언트에서 요구하는 다른 인터페이스로 변환한다. 인터페이스가 호환되지 않아 같이 쓸 수 없었던 클래스를 사용할 수 있게 돕는다.
  - Turkey를 Duck 사이에 끼워넣고 싶다면, Duck 인터페이스를 구현하는 어댑터를 만들어, Turkey 클래스를 끼워넣으면 된다. Turkey 객체를 어댑터로 감싸서, Duck 객체처럼 보이게 할 수 있다. 중요한 것은, 기존의 코드를 변경하지 않고 두 코드를 연결할 수 있다는 것이다. 협력사와 협업할 때 반드시 필요한 패턴인 것 같다. 이런 경우에, 특히 기존 코드와 새 코드가 섞여, 제대로 동작하지 않는 것에 대한 고민을 하게 되는데, 두 인터페이스를 모두 지원할 수 있도록 인터페이스가 여러 형태를 지원하면 된다고 한다. 기존의 코드와 새 코드를 모두 가져갈 수 있어서 매우 편리하고 유용한 패턴인 것 같다. 
  - 객체 어댑터와 클래스 어댑터: 클래스 어댑터는 타깃과 어댑티 모두 서브 클래스로 만들어서 사용하고, 객체 어댑터는 구성으로 어댑티에 요청을 전달한다는 점만 다르다. 객체 어댑터는 말그대로 인터페이스로 한번 감싸서 객체를 가져다 사용할 수 있게 하는 것을 의미하고, 클래스 어댑터는 타깃과 어댑티 모두를 서브 클래스로 만들어서 사용한다는 것을 의미한다. 이해한 바가 맞을까?
- 퍼사드 패턴: 서브 시스템에 있는 일련의 인터페이스를 통합 인터페이스로 묶어준다. 고수준 인터페이스도 정의하므로, 서브시스템을 더 편리하게 사용할 수 있다.
  - 퍼사드 패턴은 인터페이스를 단순하게 바꾸려고 인터페이스를 변경한다. 여러 기능들을 하나의 메소드로 묶어주는 역할을 할 뿐인 것 같다. 장점은, 간편하게 메소드를 가져다 쓸 수 있는 것과, 언제든지 서브 시스템에 직접 접근할 수 있는 것?
- 최소 지식 원칙: 다른 객체와으이 상호작용 수를 줄여야한다. 객체 사이의 의존성을 줄일 수 있으며, 소프트웨어 관리가 더 편해진다.
  - 거쳐가는 클래스를 최소한으로 줄여야한다. 파도타기 처럼 호출하지 말고, 서브 시스템 안에서 구현하고, 그것을 불러올 것! `a.callB().callC()` 가 아닌, `a.Call(C)` 가 될 수 있게!

## 8장. 템플릿 메소드 패턴

지금까지 배운 패턴 중, 가장 쉬운 패턴인 것 같다. 추상화 클래스를 만들고, 그것을 어떤 단위로 감싸서 레이어를 만드느냐가 관건인 것 같다. Tea/Coffee > Beverage > (템플릿 메소드) 로 간략화할 수 있는 것 같다. 템플릿 메소드는 말그대로 공통적인 절차를 추상화한 클래스이고, Beverage는 Tea, Coffee 등에서 볼 수 있는 공통부를 구현하고, tea/coffee 클래스는 Beverage를 가져다가 자신만의 클래스로 구현하게 된다. 다른 패턴들에서는 이러한 Tea, Coffee 클래스에 다른 기능을 추가한다거나, 두 종류의 Beverage를 섞는다거나 하는 꽤 복잡한 패턴인 것에 비해 이 패턴이 간략한 것을 보아, 이 패턴이 강력하면서도 한정적으로 사용될 수 있을 것 같다는 생각이 들었다.

## 9장. 반복자 패턴과 컴포지트 패턴

일단 **반복자 패턴**은 대부분의 자료구조가 iterator를 가지고 있다는 것을 활용하여 인터페이스를 통일하는 간결한 방법이다.
iterator를 사용할 수 없다 하더라도, iterator를 구현하여 사용할 수 있으므로 모든 자료구조에 대해 적용이 가능하다.
자료구조에 상관없이 객체 접근방식을 통일시킬 수 있다는 장점이 있다.(다형성)
이렇게 인터페이스를 통일하면 아랫단에 무엇이 있는지, 어떻게 동작하는지 알 필요를 없앨 수 있다.(캡슐화)
집합체 안의 모든 항목에 접근할 때 편리한 방식이다.
printMenu에 iterator를 넘겨주는 방식이므로, 인자를 추가하여 모든 항목이 아닌 원하는 항목에만 접근하는 것도 가능할 것 같다.  

반복자 패턴만 사용하면, A라는 자료구조를 B라는 자료구조 속에 넣을 수 없어서 추가적인 수정이 어렵다.
기존 방식을 통해 수정하기 위해서는 추가하려는 자료구조 속에서 데이터를 뽑아서 일일히 addItem 해줘야하므로, 이를 해결하기 위해 리팩터링을 실시한다.  
**컴포지트 패턴**은 트리구조를 통해서 부분-전체 계층구조를 구현할 수 있다.
부분-전체 계층구조는 부분들이 계층을 이루고 있지만 모든 부분을 묶어서 전체로 다룰 수 있는 구조를 뜻한다.
그런데, 결국에 컴포지트 패턴으로 리팩토링하기 위해서는 추가하는 A라는 자료구조를 하나씩 반복적으로 꺼내서 트리에 추가해야하지않나..라며... 이건 반복자 패턴을 처음에 사용하려 했던 취지와 맞지 않는 것 같다는 생각도 들었다.

## 10장. 상태 패턴

경우의 수나 절차에 대한 설계가 제대로 이루어진 후에야 써야할 것 같다.
자칫하다가는 어디서 꼬였는지도 모르게 꼬일 수 있을 것 같다.
인터페이스(행동)를 함수로 만들어주고, 상태에 따라 다른 액션을 취하는 코드를 보고난 후에,
상태에 따라 객체를 골라서 상태를 나타내는 객체 내의 인터페이스(함수)를 사용하는 코드를 보니까, "이렇게 생각할수도 있구나"하고 감탄했다.
- 패턴
  - 상태패턴: 상태를 기반으로 하는 행동을 캡슐화하고 행동을 현재 상태에게 위임합니다.
  - 전략패턴: 바꿔 쓸 수 있는 행동을 캡슐화한 다음, 실제 행동은 다른 객체에 위임합니다.
  - 템플릿 메소드 패턴: 알고리즘의 각 단계를 구현하는 방법을 서브클래스에서 구현합니다.  

책에서 각 패턴에 대한 설명을 위와 같이 기재해두었다. 사실 이렇게 적어두니까 무슨 말인지 이해가 더 안되는 것 같아, 웹사이트를 뒤져보았다.  
[블로그](https://jaeseongdev.github.io/development/2021/02/13/%EC%A0%84%EB%9E%B5_%ED%8C%A8%ED%84%B4%EA%B3%BC_%EC%83%81%ED%83%9C_%ED%8C%A8%ED%84%B4%EC%9D%98_%EC%B0%A8%EC%9D%B4%EC%A0%90/)를 참고하니, 아래와 같이 차이점을 설명하고 있다.  

- 전략 패턴은 한 번 인스턴스를 생성하고 나면, 상태가 거의 바뀌지 않는 경우에 사용한다.  
- 상태 패턴은 한 번 인스턴스를 생성하고 난 뒤, 상태를 바꾸는 경우가 빈번한 경우에 사용한다.

생각해보면 전략패턴을 말할때, 여러 오리의 종류를 만들고 이를 편하고 쉽게 구현/확장시키기 위해서 전략패턴을 사용한다고 했었다.  
오리의 상태는 한번 정해지면 변하지 않지만, 뽑기 기계는 동작에 따른 상태가 변한다는 점이 다르다고 생각이 들었다.

## 11장. 프록시 패턴

프록시 패턴은 {클라이언트 힙}(클라이언트 객체)-(클라이언트 보조객체) <--> (서비스 보조 객체)-(서비스 객체){서버 힙} 의 형태를 갖춘다.  
클라이언트 객체는 진짜 서비스 메소드를 호출한다고 생각하지만, 실제로는 클라이언트 보조 객체(프록시)가 작업을 맡게된다.  
클라이언트 보조 객체는 서버에 연락을 취하고, 메소드 호출에 관한 정보를 전달하고, 서버로부터 리턴되는 정보를 기다린다.  

서비스 보조 객체(원격 프록시)는 서비스 객체(원격 객체)의 로컬 대변자 역할을 한다.  
서비스 객체(원격 객체)는 다른 JVM의 힙에서 살고있는 객체(다른 주소 공간에서 돌아가고 있는 객체)이다.  
로컬 대변자는, 로컬 대변자의 어떤 메소드를 호출하면, 다른 원격 객체에게 그 메소드 호출을 전달해주는 객체이다.  
서버 단의 보조 객체가 이 연락을 받으면, 호출 정보를 해석해서 진짜 서비스 객체에 있는 진짜 서비스 메소드를 호출한다.  

자바 RMI(Remote Remote Method Invocation)?  
- 개발자 대신 클라이언트와 서비스 보조 객체를 만들어준다.
- 네트워킹 및 입출력 기능이 필요하다.(state 객체를 직렬화, 역직렬화를 사용하여 통신)
- RMI에서 클라이언트 보조 객체는 stub, 서비스 보조객체는 skeleton이라고 부른다.

## 12장. 복합 패턴

복합 패턴은 2개 이상의 패턴을 결합하는 방법이다. 오리 예제에서 클래스를 계속 감싸고 감싸는 과정이 복잡한데, 그림을 그려 따라가면 호출 과정이 이해가 될락말락...  
MVC(모델-뷰-컨트롤러)는 옵저버, 전략, 컴포지트 패턴으로 이루어진 복합 패턴이다.
- 옵저버 패턴(모델): 상태가 변경되었을 때, 그 모델과 연관된 객체들에게 연락한다. 옵저버 패턴을 사용하여 모델을 뷰/컨트롤러로부터 완전히 독립시킬 수 있다. 작업을 처리하거나, 현재 상태를 알아내는 역할을 한다.
- 컴포지트 패턴(뷰): 화면만 갱신하는 역할. 사용자가 모델과 어떤 상호작용을 하는지는 모른다.
- 전략 패턴(컨트롤러): 인터페이스의 행동을 결정한다. 사용자가 요청한 내역을 처리하기 위해 모델과 상호작용한다. 사용자 입력을 바탕으로 모델에 적절한 요청을 전달한다.

*오랜만에 여러 패턴을 리뷰하려다보니 머리가 아프다!*  

## 13장. 실전 디자인 패턴

## 14장. 기타 패턴
