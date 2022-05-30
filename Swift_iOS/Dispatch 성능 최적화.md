# Dispatch 성능 최적화
  
## Dispatch  
Dispatch는 어떤 메소드를 호출할 것인가를 결정하여 그것을 실행하는 과정이다.  
Dispatch는 Static Dispatch, Dynamic Dispatch 두 가지가 있다.  
두 개의 차이점은 호출할 함수를 Runtime, CompileTime중 언제 결정될 것인가 차이.  
  
## Static Dispatch (Direct Call)  
Static Dispatch는 컴파일 타임에 컴파일러가 어떤 메소드를 실행할지 주소값을 알고 있기 때문에, 별도의 과정이 필요없고 inline으로 수행되므로 빠르다.  
하지만 서브 클래싱의 장점을 이용하지 못한다.  
  
## Dynamic Dispatch (Indirect Call)
OOP를 기반으로 둔 언어가 Dynamic Dispatch 방법을 사용한다.(다형성에서 Dynamic Dispatch로 접근)  
런타임에 호출될 함수를 결정하기에 Swfit에서는 클래스마다 vtable(Virtual Dispatch Table)을 가지고 있다.  
vtable는 함수 포인터들의 배열로 표현되며, 하위 클래스가 메소드를 호출할 떄 이 배열을 참조하여 실제 호출할 함수를 결정한다.  
vtable를 참조하여 함수를 호출하기에 이에 따른 overhead가 발생하여 Static Dispatch보다 성능적으로 손해.  
  
## Swift에서의 Static, Dynamic Dispatch
**Value Type**  
struct ,enum와 같은 값 타입에서는 상속이 불가능 하기에 Static Dispatch로 동작한다.  
  
**Reference Type**  
참조 타입인 class는 상속의 가능성이 존재하기에 Dynamic Dispatch로 동작한다.  
하지만 오버라이딩 되지 않는다는 것을 컴파일러가 알 수 있다면, Static Dispatch로 동작한다.  
  
**Protocol**  
프로토콜은 구현체는 제공하지 않고, 선언부만 제공한다.  
실제 사용할 때 프로토콜 타입을 참조로만 사용할 경우 해당 인스턴스 타입에 맞는 메서드를 호출해야해서 Dynamic Dispatch로 동작한다.  
  
**extension**  
일반적인 경우 extension을 통해 메서드 오버라이딩이 불가능하다.  
그렇기에 Value Type, Reference Type에서 extension에서 추가된 메서드를 호출할 경우 Static Dispatch로 동작한다.  
  
Protocol에서의 esxtension 설명하기 전에 Witness Table에 대해 설명한다.  
Witness Table란 프로토콜을 통해 호출하는 메소드는 프로토콜을 채택한 타입들이 실제로 구현한 메소드이므로, 프로토콜 타입의 참조로만 구현체의 내용을 사용할 때 사용되는 프로토콜이 보유한 정보를 `Witness Table`이라 명칭한다.  
  
Protocol에서의 esxtension의 경우는 두 가지가 있다.  
1. 본체에 선언된 멤버의 디폴트 구현체: 서브 클래스들이 메소드들을 구현하고 있음이 보장되므로, Witness table을 이용한 Dyanamic Dispatch 수행  
2. 본체에 없는 기능을 추가한 경우 : 본체에 선언하지 않고 extension으로 추가한 메소드들은 Witness Table을 이용할 수 없습니다. 즉, Dynamic Dispatch를 사용할 수 없고, Static Dispatch가 적용된다.  
  
## Dispatch를 통한 성능 최적화
**final**  
class에 final 키워드가 붙으면 상속이 불가능하며, 프로퍼티나 메서드에 붙을 경우 하위 클래스에서 오버라라이딩 불가.  
그렇기에 Static Dispatch로 동작한다.  
상속, 오버라이딩이 될 필요가 없는 클래스, 메서드, 프로퍼티에 final키워드를 붙여 성능 최적화.  
  
**private or fileprivate**  
private or fileprivate 키워드를 붙여서 선언할 경우 한블럭 내에서만 참조되는 것이 보장되기에, 한 블럭내에 오버라이드가 없는 경우 Static Dispatch로 동작한다.  
  
**Value Type**  
서브 클래싱이 불가능한 Vlaue Type를 사용하여 Static Dispatch가 이루어지도록 한다.  
  
**WMO(Whole Module Optimization)**  
기본적으로 Swift는 각 파일을 개별적으로 컴파일하기에 Xcode는 여러 파일을 병렬로 매우 빠르게 컴파일 할 수 있다.
그러나 각 파일을 개별적으로 컴파일하면 최적화 기법을 사용할 수 없다.  
Swift는 여러 파일을 하나의 파일처럼 컴파일하고 최적화하는 기능도 지원하는데 이러한 모드는 commnad line flag인 whole-module-optimization 에서 활성화 할 수 있다.  
WMO를 사용하면 전체 파일을 한번에 컴파일 하기에 internal이 override되는것을 확인할 수 있고, override 되지 않는다면 자동으로 final을 붙여 dynamic dispatch를 줄일 수 있다.  
하지만 WMO는 빌드 시에 모든 파일을 한번에 분석하여 static dispatch 변환 가능성 판단하여 최적화 하나 몹시 느리고 안정화가 안되므로 사용에 주의 필요하다.  
  
