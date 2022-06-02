# guard let self = self 에 대해
  
Closure내부에서 self를 캡쳐할 때  non-optional일 경우,  
Closure 시작 부분에 `guard let self = self else { return }`를 쓰는 경우가 있다.  
`guard let self = self`의 의미는 클로저 내에서 외부 프로퍼티를 캡쳐할때, 현재 instance가 heap영역에 존재하면 객체를 Strong로 참조하고, instance가 해제 되었으면 nil을 반환하여 탈출한다는 의미이다.  
  
## `guard let self = self`을 사용할 때 야기할 수 있는 문제점
1. `guard let self = self`을 사용했을 경우에는 강한참조가 유지되어서, 클로저내에 무거운 작업이 있다면 crash가 발생할 수도 있어서 `guard let self = self`구문을 지양해야 한다.  
2. `deallocation delay` 발생 문제  
클로저 안에서 이미지를 로드 하는 등의 시간이 오래 걸리는 작업이 있다면 클로저 안의 로직을 수행하는 도중에 self 인스턴스가 해제될 수 있다.  
그런데 guard let으로 self 를 체크하면 self에 대한 강한 참조가 생기고 이후 클로저가 종료될 때까지 self의 해제를 지연시킨다.  
```Swift
func process(image: UIImage, completion: @escaping (UIImage?) -> Void) {
    DispatchQueue.global(qos: .userInteractive).async { [weak self] in
        guard let self = self else { return }
        // perform expensive sequential work on the image
        let rotated = self.rotate(image: image)
        let cropped = self.crop(image: rotated)
        let scaled = self.scale(image: cropped)
        let processedImage = self.filter(image: scaled)
        completion(processedImage)
    }
}
```
위 코드를 예로 살펴보면,  
guard let self = self 로 self 를 체크했기 때문에 클로저 안에서는 self에 대한 강한 참조가 생기고
self는 해당 클로저가 종료될때까지 메모리에서 해제되지 않는다.  
하지만 image 처리 관련된 무거운 로직이 실행되는 도중에 viewController는 언제든지 해제될 수 있다.  
이때 viewController가 dismiss 되어도 클로저에서 강한 참조로 잡고 있기 때문에 클로저가 종료될때까지 viewController는 메모리에세 해제될 수 없다.  
  
viewController 가 해제된 이후에 불필요한 작업이 진행되는 것을 피하고 싶다면 → self?.  
반대로 객체가 해제되기 전에 모든 작업을 완료하고 싶다면 → guard let  
  
  
  
  
  
참고
https://jinsangjin.tistory.com/129
https://ios-development.tistory.com/602
