# MVVM Model - View - View Model
  
MVVM패턴은 MVP패턴에서 파생되어 나왔으며, 3가지의 구성 요소를 가지고 있다.  
1. 모델 (Model)  
2. 뷰 (View)  
3. 뷰 모델 (View Model)  
   
#### Model
Model은 데이터와 관련된 코드를 담고 있다.  
데이터를 어떻게 가지고 있을지만 알고있으면 된다.  
  
#### View
앱의 UI에 대한 코드를 담고 있다.  
View의 각 컴포넌트에 대한 정보와 어느위치에 배치될지 작성되어 있으며, ViewModel로부터 데이터를 가져와서 어떻게 배치할지 특정상황에 따라 ViewModel의 어떤 메서드를 이용할지에 대해서도 가지고 있다.  
View는 재사용성이 강조되며, 중복된 코드를 최소화하는 것이 중요하다.  
  
#### ViewModel
앱의 핵심적인 비즈니스 로직을 담고 있는 코드 계층이다.  
View와 Model사이에서 View의 요청에 따라 로직을 실행하고, Model의 변화에 따라 View를 refresh하거나, Model에 변화가 생기면 View에게 notification을 보내주는 역할을 한다.  
View Model은 UI관련 코드로부터 완전히 분리되어 있다.  
  
## MVVM + Coordinator
iOS에서는 화면전환이 필요할때 크게 두 가지를 이용한다.  
ViewController을 직접 Present하는 방법.  
UINavigationController을 이용한 화면 이동.  
ViewController에서 유저의 행동에 따라 화면전환이 이루어지는데, 이때 코드로 직접 위의 두 가지 방법을 사용하거나 Story board 상의 Segue를 연결하여 화면전환을 한다.  
코드를 이용한 화면전환은 Present, Navigation에 Push 하는 형태일 것이다.  
MVVM을 적용한 화면이라면 화면전환은 ViewController에서 일어나게 될텐데, 화면 관리에 대한 추적이 매우매우 힘들어진다.  
새롭게 만들어진 ViewController에 ViewModel을 주면 해당 화면이 어디서 생성되었고 언제 ViewModel이 주입되었는지를 추적하려면 선언부를 찾아가야한다.  
이게 ViewController(이하 VC)이곳 저곳 필요한 곳에 아무렇지 않게 선언되어 사용된다면, 처음엔 쉽고 편하지만 점점 해당 VC를 사용하는 곳이 많아지면 찾기가 힘들어진다.  
화면의 관리를 해주는 객체, 방법 이게 Coordinator Pattern 이다.  
더불어 VC가 다른 VC를 만들때의 의존성을 Coordinator에게 위임하다 보니 느슨한 결합을 할 수 있으며, 코드의 재사용성이 더 높아진다.  
  
#### MVVM + Coordinator의 장점
화면 VC는 그 화면에서의 이벤트 처리만 보여주게 되었고, 화면전환이 여기서 어떻게 이루어지고 결과를 어떻게 넘기는지는 해당 Coordinator만보면 단번에 알아 볼 수 있고 코드의 흐름을 파악하기에도 쉬워졌다.  
그리고 앞서말한 VC의 다른 ViewModel간의 결합도도 낮아진다.  
  
  
  
  
---
출처  
https://medium.com/nbt-tech/mvvm-그리고-coordinator-a8d4f9d0fc8a
