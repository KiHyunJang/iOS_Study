# Type Annotation과 Type Inference의 성능 차이
  
## Type Annotation
```Swift
let z: Int = 100
var x: Int
```
Type Annotation일 경우, 위와 같이 초기값이 없어도 되며 자료형을 명시하는 방법.  
  
## Type Inference
```Swift
let a =" 1"
var b = "22"
```
위와 같이 타입을 선언하지 않을 경우 값을 보고, 형식을 알아서 추론하여 지정한다.  
이를 Type Inference이라고 한다.  
Swift에선 Character나 String 모두 큰따옴표를 통해 나타내기에 a를 Character를 나타내고 싶었어도 String가 된다.  
Type Inference될 때, 무조건 더 큰 자료형으로 지정한다.
ex) Character -> String, Float -> Double  

`Type Inference`방법은 컴파일러가 타입을 추론하는 과정에서 오버헤드가 발생하기에, `Type Annotation`방법을 통해 변수를 선언하는 것이 성능상 이점을 가져온다.
