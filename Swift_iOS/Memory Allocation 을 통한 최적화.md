# 인스턴스 생성 시 Memory Allocation 고려를 통한 성능 최적화
  
## Memory Allocation
메모리의 할당과 헤제는 `Stack`과 `Heap`에서 처리된다.  
`Stack`은 LIFO의 단순한 구조로 Stack Pointer를 사용하여 메모리할당과 헤제가 빠르게 이루어진다.
`Heap`은 Stack보다 더 복잡한 구조로 Heap영역에서 적절한 블록을 찾아 메모리할당과 해제가 이루어지기 때문에 상대적으로 느리다.  
그리고 `Heap`은 동기화 문제가 발생할 수 있기에 무결성을 보호해야한다는 단점이 있다.
  
## Heap 할당 피하기
```Swift
enum Alcohol { case soju, cocktail, wine, Makgeolli, beer }
enum Place { case bar, home, park, hotel }

var cachedImage = [String: UIImage]()

func generateImage(_ alcohol: Alcohol, _ place: Place) -> UIImage {
    let key : String = "\(alcohol):\(place)"
    if let image = cachedImage[key] {
        return image
    }
    ...
}
```
위 코드는 술과 장소를 전달하면 받은 전달인자를 구분해 사진을 반환하는 동작을 한다.  
전부 값 타입을 써서 Stack에서 동작이 이루어지는 것같지만,  
String가 값 타입이지만 String의 요소들은 Heap에 할당되기에 Heap할당이 발생한다.  
성능을 개선하려면 어떻게 해야할까?  
Heap할당을 발생시키는 String를 처리해줘야할 것이다.  
  
```Swift
enum Alcohol { case soju, cocktail, wine, Makgeolli, beer }
enum Place { case bar, home, park, hotel }
struct Attribute: Hashable {
    var alcohol : Alcohol
    var place : Place
}

var cachedImage = [Attribute: UIImage]()

func generateImage(_ alcohol: Alcohol, _ place: Place) -> UIImage {
    let key : Attribute = Attribute(alcohol: alcohol, place: place)
    if let image = cachedImage[key] {
        return image
    }
    ...
}
```
딕셔너리의 key타입을 String에서 Struct인 Attribute로 대체했다.  
이를 통해 generateImage 호출 시 발생하던 Heap 할당을 제거해서 성능을 개선할 수 있다.  
  
  
  
  
  
참고  
https://velog.io/@yohanblessyou/Apple-Understanding-Swift-Performance  
https://corykim0829.github.io/swift/Understanding-Swift-Performance/#
