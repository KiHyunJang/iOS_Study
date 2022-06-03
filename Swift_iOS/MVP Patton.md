# MVP (Model - View - Presenter)
Model - View - Presenter 로 이뤄진 디자인 패턴이며 MVC에서 Controller가 하는 역할을 Presenter가 한다.  
MVC는 Model과 View가 서로 연결되어 있어 의존관계를 갖게 되고, MVP패턴을 사용한다면 Model과 View가 분리되어 오직 Presenter를 통해 변화를 알려줄 수 있다.  
  
### MVP패턴의 뷰 업데이트 과정
1. View에 사용자의 인터랙션이 들어온다.  
2. View는 Presenter에 액션이 들어왔다고 전달한다.  
3. Presenter는 View 액션대로 Model을 구성한다. (보통 Service를 가지고 있고 요청하는 경우가 많습니다.)  
4. Update된 Presenter의 데이터를 View에 업데이트 합니다.  
  
#### Model
Model은 데이터와 관련된 코드를 담고 있다.  
데이터를 어떻게 가지고 있을지만 알고있으면 된다.  
  
#### View
앱의 UI에 대한 코드를 담고 있다.  
View의 각 컴포넌트에 대한 정보와 어느위치에 배치될지 작성되어 있으며, ViewModel로부터 데이터를 가져와서 어떻게 배치할지 특정상황에 따라 ViewModel의 어떤 메서드를 이용할지에 대해서도 가지고 있다.  
View는 재사용성이 강조되며, 중복된 코드를 최소화하는 것이 중요하다.  

### Protocol
Presenter에 필요한 함수나 변수 등을 정의.
  
### Presenter
Protocol에서 정의한 함수와 변수들을 구현.  
보통 Service를 가지고 있고 View에서 받은 인터랙션대로 요청하여 Presenter의 데이터를 변경.  
View에 필요한 데이터 character를 가지고 있고 View에서 일어나는 액션에 따라 데이터가 바뀌게끔 구현.  

### MVP의 장점
View와 비즈니스 로직이 분리되어 있어 Test에 용이하다.  

### MVP의 단점
어플리케이션이 복잡해질수록 View와 Presenter 사이의 의존성이 강해지는 문제가 있습니다. MVC의 Controller처럼 추가 비즈니스 로직에 집중되는 경향이 있다.  
 개발자는 오랜 시간 앱을 개발하는 어느 순간, 거대해지며 문제가 발생하기 쉽고, 분리하기 어려운 Presenter를 발견하게 된다.  
  
  
  
  
참고
https://fomaios.tistory.com/entry/Design-Pattern-MVP-패턴이란
