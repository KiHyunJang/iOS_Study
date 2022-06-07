# 의존성 주입(Dependency Injection)
  
## 의존성
```Swift
class SomeController {
    var fooManager = FooManager()
}
```
SomeController는 FooManager 클래스에 대해 의존관계가 생김
  
## 의존성 주입이란?
어떤 객체가 다른 객체의 의존성을 제공하는 기술이다.  
또한 객체의 생성과 사용의 관심을 분리하는 것을 의미.  
의존성 주입을 통해 프로그램의 디자인의 결합도를 느슨하게 할 수 있고, 의존관계 역젼원칙과 단일 책임원칙을 따르도록 설계가 가능하다.  
  
만약 두 개의 클래스가 있다고 가정. (A, B)  
B를 사용하기위해 A에서 사용해야하는 경우, A내에서 객체를 직접 생성하여 사용할 수 있다.  
이러한 경우에 A는 B에 의존하게 된다. (의존성을 가지는 관계)  
  
위 경우 설계에 문제점 발생.  
의존관계를 만들게되면 이후에 객체 B로부터 독립적으로 인스턴스의 생성을 변경하는 것이 불가능해지기에 유연하지 않은 설계로 이어진다.  
이러한 상황을 방지하기 위해 의존성 주입 사용.  
간단하게 말하자면, 외부에서 초기화해서 클래스 내부에 할당해주는 것이다.  
  
## 의존성 주입의 원리
- 다른 객체 B를 호출하려는 객체 A는 객체 B가 어떻게 구현되어 있는지 알지 못해야한다.
- 대신 객체 B에 대한 책임을 외부코드 또는 주입자로 위임해야한다.
- 객체 A는 주입자를 호출할 수 없다.
- 주입자는 객체 B를 객체 A에게 전달한다.
- 객체 A는 객체 B를 사용할 수 있게 된다.
  
## 의존성 주입 조건 3가지와 장점
1. 클래스 모델이나 코드에 런타임 시점의 의존관계가 드러나지 않는다.  
2. 런타임 시점의 의존관계는 제 3의 존재(Factory 등)에 의해 결정되어야 한다.  
3. 의존 관계는 사용할 오브젝트에 대한 레퍼런스를 외부에서 제공해줌으로써 만들어진다.  
  
장점으로는 생성된 객체를 인터페이스를 통해 넘겨받기 때문에 결합이 느슨해지고,
런타임 시에 의존관계가 결정되기에 유연해진다.

## 의존성 주입 방법 3가지

### Initializer Injection
```Swift
class SomeController {
    
    var fooManager: FooManager
    
    init(fooManager: FooManager) {
        self.fooManager = fooManager
    }
}

let manager = FooManager()
var someController = SomeController(fooManager: manager)
```
  
### Property Injection
```Swift
class SomeController {
    
    var fooManager: FooManager?
}

let manager = FooManager()

var someController = SomeController()
someController.fooManager = manager
```
  
### Method Injection
```Swift
class SomeController {
    
    var fooManager: FooManager?
    
    func fooManager(using manager: FooManager) {
        self.fooManager = manager
    }
}

var someController = SomeController()
someController.fooManager(using: FooManager())
```
