# MVC (Model - View - Controller) 
MVC 패턴은 Model - View - Controller 로 구성된 사용자 인터페이스, 데이터 및 논리 제어를 구현하는데 널리 사용되는 소프트웨어 디자인 패턴이다.  
우리가 개발을 할 때 3가지 형태로 역할을 분할하여 개발하는 방법론이다.  
  
## MVC패턴의 장점 및 단점
**장점**  
비즈니스 처리 로직과 사용자 인터페이스 요소들을 분리시켜 서로 영향없이 개발과 유지보수를 상대적으로 쉽게한다는 장점이있고, 다른 아키텍쳐 패턴에 비해 단순하다.  
  
**단점**  
View와 Model가 서로 의존성이 높다.  
그렇기 때문에, 어플리케이션이 복잡해지고 커질수록 유지보수가 어렵다.  
​  
## 각각의 역할
**Model**  
모델은 앱이 포함해야할 데이터, 데이터의 상태 변경 등을 관리하며, 무엇을 할 것인지를 정의한다.  
ex) DB와의 상호작용, 처리되어야할 알고리즘 등등  
​  
**View**  
뷰는 화면에 무엇을 보여줄것인지 정의합니다.  
컨트롤러의 하위에 종속되어 모델이나 컨트롤러가 보여주려고 하는 모든 필요한 것들을 보여줍니다.  
ex) UILabel, UIButton등등  
  
**Controller**  
컨트롤러는 모델이 어떻게 처리할 것인지를 알려주는 역할을 하고, 화면의 로직처리를 합니다.  
ex) iOS App개발시 TableViewDataSource프로토콜이 cell을 어떻게 보여줄 건지 등등  
  
## MVC의 동작 방식
1. 사용자가 View를 통해 interface를 한다.  
2. controller가 Model에게 데이터를 전달한다.  
3. Model이 전달받은 데이터를 통해 state을 변경한다.  
4. 변경된 state를 View에게 전달한다.  
5. View에서 이벤트 결과 확인.  