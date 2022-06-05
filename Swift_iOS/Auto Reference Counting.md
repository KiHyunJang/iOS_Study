# ARC(Auto Reference Counting)
  
## ARC?
Swift는 앱에서 메모리 사용을 관리, 추적하기 위해서 ARC를 사용한다.  
매번 값을 복사해서 전달하는 값 타입과 달리 참조 타입의 경우에 하나의 인스턴스가 참조를 통해 여러 곳에서 접근하기 때문에 언제 메모리에서 해제되는지가 중요하다.  
인스턴스가 적절한 시점에 메모리가 해제되지 않으면 메모리 자원을 낭비한다.  
그렇기에 swift에선 ARC를 사용한다.  
  
ARC는 참조 타입인 클래스의 인스턴스에만 적용되며, compile time에 실행되어 제거 시점을 파악하기위해 소유자 수를 저장하는데 이것을 Reference Count 라고한다.  
참조 카운트가 1 이상이면 메모리에서 유지되며, 0 이 되면 메모리에서 제거한다.  
코드 레벨로 보자면 Reference Count가 증가할 때는 해당 인스턴스의 retain 메소드를 호출하는 것과 같으며, 소유권을 포기하여 메모리에서 제거될 때는 release 메소드를 호출하는 것과 같다.  

## Strong
일반적인 참조(포인터와 같은 것들)이지만 ARC에 의해 해제되지 않도록 reference count을 1 증가시킨다는 점에서 특별하다.  
일반적으로 어떠한 것이 객체를 strong 참조하는 동안 객체는 해제되지 않는다.  
  
property 선언에서 default로 strong 참조를 가진다.  
일반적으로 객체의 계층이 선형적 으로 이루어져 있을 때 안전하게 사용할 수 있다.  
부모에서 자식으로 강한 참조 관계일 때 항상 안전하다.  
  
## Weak
weak 참조는 ARC로 부터 객체가 해제되는 것을 막지 않는다.  
또한 객체가 할당 해제되면 포인터는 nil이 되며, 이렇게 하면 weak 참조는 항상 객체에 접근할 때 유효한 객체이거나 nil이거의 상태가 된다.  
  
모든 weak 참조 변수는 let이 아닌 var여야 한다.  
→ 참조되고 있지 않은 객체는 nil로 변경되기 때문 (mutable)  
  
weak 참조는 retain cycle이 일어날 가능성이 있을 때 사용하는 것이 중요.  
두 객체가 서로를 strong하게 참조하고 있으면, ARC는 두 객체에 적절한 release message를 전달할 수 없습니다.  
  
예를 들어, 클로져 범위 밖에 변수가 선언되어 있고, 클로져 범위 내에서 그 변수를 참조하면 또 다른 strong 참조가 생성되게 된다.  
단, value semantics(Ints, Strings, Arrays, Dictionaries 등)를 가지는 것들은 예외.  
  
weak reference는 객체의 lifetime에 nil이 될 수 있는 경우, 반대로 참조가 nil이 되지 않을 때 즉, 참조하고 있는 객체와 같거나 더 긴 lifetime을 가지고 있을 때는 unowned reference를 쓰라고 apple 문서에 적혀있다.  
  
## Unowned
unowned는 weak와 유사하게 reference count를 증가시키지는 않지만, optional 값이 아니라는 이점을 가지고 있다. 이는 optional binding의 수고를 덜어준다.  
  
객체가 해제되고 나면, dagling pointer가 된다.  
  
클로저가 서로 상호의존적일 때 (하나가 다른 하나 없이는 live할 수 없을 때), weak 보다는 unowned를 쓰는 것이 프로그램이 불필요하게 nil 참조를 유지하는 overhead를 막아준다.  
  
## 강한 순환 참조 문제
ARC(Automatic Reference Counting)는 Person 인스턴스에 대한 참조의 개수를 트래킹 하고, Person 인스턴스가 더 이상 필요하지 않게 되면(참조가 0이 되면) deallocate 시킨다.  
만약 두 클래스 인스턴스가 서로에 대해 강한 참조를 통해 각 인스턴스가 다른 인스턴스를 유지하게 되는 경우가 존재하는데, 이 경우를 강한 순환 참조(strong retain cycle)이라고 한다.  
ARC는 이러한 강한 순환 참조(strong retain cycle)에 대한 메모리 관리를 해주지 않기 때문에 약한 참조(weak reference), 비소유 참조(unowned reference)를 통해 직접 사용해서 해결해야한다.  
  
  
  
  
  
참고  
https://velog.io/@rnfxl92/Strong-Weak-Unowned
