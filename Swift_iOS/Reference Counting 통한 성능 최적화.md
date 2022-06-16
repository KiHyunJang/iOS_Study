# Reference Counting 고려를 통한 성능 최적화
  
## Reference Counting Overhead
Swift에서는 Heap에 할당된 메모리를 언제 해제해야 할지 판단하기 위해서 Reference Count를 사용하는데,   
Heap에 할당되는 인스턴스는 Reference Count관리가 필요하다.  
여러 스레드에서 동시에 Reference Count를 증감시킬 수 있기에 Thread-safety overhead도 중점적으로 봐야한다.  
  
  
## Reference Counting in Struct
Heap 할당이 일어나지 않는 struct에서는 Reference Count가 발생하지 않는다 생각할 수 있지만,  
Struct가 reference semantics를 따르는 타입을 프로퍼티로 갖게 된다면 Reference Count가 발생한다.  
만약 구조체 내에 이렇게 레퍼런스를 가지게되면 Reference Counting Overhead 비용이 발생한다.  
그래서 만약 구조체에 있는 레퍼런스 개수에 비례하는데, 하나보다 많은 레퍼런스를 갖게된다면,  
Reference Counting Overhead 비용이 class보다 더 많이 발생하게 된다.  
  
  
## Reference Counting Overhead 최소한으로 줄이기
1. 값 타입내에 프로퍼티중 참조타입을 값타입으로 변경할 수 있다면 변경하기
2. 값 타입내에 String같이 간접적으로 참조타입을 사용하는 프로퍼티를 extension을 통해 guard문 쓰기  
  
  
  
  
  
  
참고  
https://velog.io/@yohanblessyou/Apple-Understanding-Swift-Performance  
https://corykim0829.github.io/swift/Understanding-Swift-Performance/#
