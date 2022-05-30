# Reference and Value types in Swift
  
### Reference types
참조 타입은 memory의 heap영역에 저장되는 타입이며, 이 데이터를 가리키는 주소값은 stack영역에 저장된다.  
이렇게 데이터를 참조하려 사용하기 때문에 값 타입과 달리 데이터를 변수에 할당하거나 함수에 전달할 때 값을 복사하지 않고 참조값을 사용한다.  
  
### reference types of swift
class, closure  
  
### Value types
값 타입은 memory에서 stack영역에 저장되는 타입이다.  
메모리에 할당된 값 타입의 데이터를 다른 변수나 상수에 복사하면, 각각의 인스턴스는 데이터의 유일한 복사값을 갖게된다.
그렇기에 복사된 인스턴스의 값을 수정해도 기존의 인스턴스에 영향이 없다.  
  
### value types of swift
struct, enum, Fundamental data types(Int, String...), Collection types(Array, Set...), value타입으로 구성된 tuple  
swift의 표준 라이브러리의 value type은 enum을 제외한 모든 타입이 struct로 구현되어 있다.  
  
### Reference types and Value types의 차이점
스택 할당(Stack allocation)과 힙 할당(Heap allocation)에는 구조적인 차이가 있다.  
stack은 한 방향으로만 데이터를 넣고 빼는 단순한 구조이기 때문에 stack pointer를 사용하여 빠르게 접근이 가능하다.  
하지만 heap은 할당할 때마다 적절한 메모리 공간이 있는지 확인을 한 후에 할당하는 구조이다.  
이러한 과정은 stack보다 heap의 할당방식이 더 복잡하기 때문에 일반적으로 더 좋은 성능의 코드를 작성하기 위해서는 value 타입을 사용하는게 유리하다.  
  
### struct와 class 중에서 어떤 것을 사용할지 정하는 기준 예시
- 상속이 필요하지 않고 모델이 크지 않으면 struct 사용  
- json파싱할 경우 struct사용  
- serialize해서 전송하거나 파일로 저장할 일이 있다면 class사용  
- Obj-C에서도 사용하려면 class사용  
`serialize ?` : 객체를 직렬화 하여, 전송 가능한 파일 형태로 만드는 것  
  
  
  
**참고**  
야곰아카데미 Reference and Value types in Swift 강의
