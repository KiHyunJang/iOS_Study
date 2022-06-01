# iOS App Life Cycle
  
### 앱이 실행되었을 때 발생하는 일
1. UIAPplication 객체 생성  
2. UIApplicationMain or @Main Annotation을 찾아 AppDelegate 객체 생성  
3. Main Event Loop 실행  
  
### 앱의 구조
iOS앱은 기본적으로 MVC구조를 사용해서 데이터와 비즈니스 로직을 UI요소로부터 분리를 시켜준다.  
이 덕분에 다른 디바이스에서도 같은 동작을 수행할 수 있다.  
  
### Main Run Loop ?
user가 발생시키는 이벤트들을 처리하는 프로세스이다.  
UIAPplication객체는 앱이 실행될 때, Main Run Loop를 실행시키고 View와 관련된 이벤트, View의 업데이트를 한다.  
이름에서 알 수 있듯이 메인 스레드에서 실행된다. (View와 관련된 이벤트를 수행하기 때문에)  
  
사용자가 디바이스에서 특정 액션을 취하면, 해당하는 이벤트가 시스템에 의해 생성되어 UIKit에서 생성한 port를 통해 앱에 전달된다.  
전달된 이벤트들은 queue에 보관되고 하나씩 Main Run Loop에 전달되어 처리가 된다.  
  
### App State
Not Running : 실행되지 않았거나, 시스템에 의해 종료된 상태  
Inactive : 실행 중이지만 이벤트를 받고있지 않은 상태. 예를들어, 앱 실행 중 미리알림 또는 일정 얼럿이 화면에 덮여서 앱이 실질적으로 이벤트는 받지 못하는 상태등을 뜻합니다.  
Active : 어플리케이션이 실질적으로 활동하고 있는 상태.  
Background : 백그라운드 상태에서 실질적인 동작을 하고 있는 상태. 예를 들어 백그라운드에서 음악을 실행하거나, 걸어온 길을 트래킹 하는 등의 동 뜻합니다.  
suspended : 백그라운드 상태에서 활동을 멈춘 상태. 빠른 재실행을 위하여 메모리에 적재된 상태지만 실질적으로 동작하고 있지는 않습니다. 메모리가 부족할때 비로소 시스템이 강제종료하게 됩니다.  
  
앱의 상태는 총 5가지이며, 대부분의 상태 전환은 AppDelegate객체의 메소드 호출을 거친다.  
  
### AppDelegate의 메소드 호출
#### 1. Not Running 상태
  
**application(_:willFinishLaunchingWithOptions:)**  
어플리케이션이 최초 실행될 때 호출되는 메소드앱을 실행할 때 최초로 실행할 코드를 작성하면 좋고, 필요한 주요 객체들을 생성하고 앱 실행 준비가 끝나기 직전에 호출  
  
**applicationDidFinishLaunching(_:)**  
어플리케이션이 실행된 직후 사용자의 화면에 보여지기 직전에 호출 주로 초기화 코드를 이곳에 작성.  
  
**applicationWillTerminate(_:)**  
어플리케이션이 종료되기 직전에 호출  
  
#### 2. In - Active 상태
  
**sceneWillEnterForefrouind(_:)**  
앱이 backfround or not running에서 foreground로 들어가기 직전에 호출된다. (비활성화 상태 -> 활성화 상태)   
  
**sceneWillResignActive(_:)**  
App Switcher 모드 (홈 바를 쓸어 올리거나 홈 버튼을 두번 눌렀을 경우)  
  
#### 3. Active 상태
  
**sceneDidBecomeActive(_:)**  
앱이 비활성화상태에서 활성상태로 진입하고 난 직후 호출되며, 앱이 실제로 사용되기 전에 마지막으로 준비할 수 있는 코드를 작성할 수 있다.  
  
#### 4.Background 상태
  
**sceneDidEnterBackground(_:)**  
앱이 Background 상태로 들어갔을 때 호출되며, suspended 상태가 되기 전 중요한 데이터를 저장하는 등 종료하기 전 필요한 작업을 한다.  
  
#### 5. Suspended 상태
  
따로 호출되는 메소드는 없으며 background 상태에서 특별한 작업이 없을 때 이 상태가 된다.  
  
---
### iOS 12 까지의 동작
iOS 12까지는 SceneDelegate가 없으며, iOS 13부터 SceneDelegate가 있다.  
Scene을 지원하지 않는 경우 모든 생명주기 관련 이벤트들은 AppDelegate에 전달이 된다.  
  
### iOS 13부터의 동작
sceneDelegate는 iOS13부터 추가된 클래스이며 UI 생명주기를 관리하는 클래스이다.  
iOS12까지는 하나의 앱이 하나의 윈도우만 가지기 때문에 AppDelegate 클래스가 UI 생명주기까지 관리했다.  
하지만 iOS13부터는 하나의 앱에 여러 개의 윈도우를 동시에 사용할 수 있게 되어서 UI생명주기를 전담 관리해줄 클래스가 필요했다.  
이를 위해 추가된 클래스가 SceneDelegate이다.  
  
즉, scene을 지원하는 경우에는 scene별로 별도의 생명주기를 갖는다.  
scene 하나는 디바이스에서 돌아가는 앱의 UI인스턴스 하나를 나타낸다.  
하나의 앱은 여러 개의 scene을 가질 수 있으며 이를 개별적으로 띄우거나 숨길 수 있다.  
