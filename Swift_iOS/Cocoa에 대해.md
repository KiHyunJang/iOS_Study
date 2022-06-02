# Cocoa, Cocoa Touch framework
  
## Cocoa & Cocoa Touch
cocoa 와 cocoa touch 둘 다 앱 개발 환경 (application environment)이다. 각각 macOS, iOS 에서 실행되는 앱을 개발하기 위한 API 이며, 이를 위한 프레임워크들을 포함한다.  
- Cocoa 는 Founcation, AppKit framework 를 포함하며 OS X에서 동작하는 앱을 개발하기 위해서 사용된다.
- Cocoa Touch는 Founcation, UIKit framework 를 포함하며 iOS에서 동작하는 앱을 개발하기 위해 사용된다.
  
## UIKit
iOS의 UI와 이벤트를 관리하는 프레임워크이다.  
UIKit 프레임워크는 제스처 처리, 애니메이션, 그림 그리기, 이미지 처리, 텍스트 처리 등 사용자 이벤트 처리를 위한 클래스를 포함합니다.  
또한 테이블뷰, 슬라이더, 버튼, 텍스트 필드, 얼럿 창 등 애플리케이션의 화면을 구성하는 요소를 포함합니다.
UIKit 클래스 중 UIResponder에서 파생된 클래스나 사용자 인터페이스에 관련된 클래스는 애플리케이션의 메인 스레드(혹은 메인 디스패치 큐)에서만 사용하세요.  
UIKit은 iOS와 tvOS 플랫폼에서 사용합니다.  
​  
#### UIKit 기능별 요소
**사용자 인터페이스**  
View and Control : 화면에 콘텐츠 표시  
View Controller : 사용자 인터페이스 관리Animation and Haptics : 애니메이션과 햅틱을 통한 피드백 제공  
Window and Screen : 뷰 계층을 위한 윈도우 제공  
​  
**사용자 액션**
Touch, Press, Gesture: 제스처 인식기를 통한 이벤트 처리 로직  
Drag and Drop: 화면 위에서 드래그 앤 드롭 기능  
Peek and Pop: 3D 터치에 대응한 미리 보기 기능  
Keyboard and Menu: 키보드 입력을 처리 및 사용자 정의 메뉴 표시  
  
Xcode에서 ViewController을 생성하면 상단에 import UIKit이 있는 것을 보았을 것이다.  
ViewController와 UIKit가 왜 함께 붙어다니냐면  
ViewController는 UIViewController를 상속 받는다.  
UIViewController는 UIKit에 정의된 클래스이고, 사용자의 인터페이스와 액션을 관리한다.  
그렇기 때문에, import UIKit를 해줌으로써 컴파일러가 UIViewController 클래스를 찾아 빌드를 해준다.  
  
## Foundation
Foundation은 원시 데이터 타입(String, Int, Double), 컬렉션 타입(Array, Dictionary, Set) 및 운영체제 서비스를 사용해 애플리케이션의 기본적인 기능을 관리하는 프레임워크다.  
Foundation프레임워크는 데이터 타입, 날짜 및 시간 계산, 필터 및 정렬, 네트워킹 등의 기본 기능을 제공한다.  
Foundation 프레임워크에서 정의한 클래스, 프로토콜 및 데이터 타입은 iOS뿐만 아니라 macOS, watchOS, tvOS 등 모든 애플 SDK에서 사용된다.  
  
Foundation에서 제공하는 데이터 타입 및 컬렉션 타입의 대부분은 Objective-C 언어의 기능에서 지원하지 않는 것이기 때문에 언어기능을 보완하기 위한 구현이며, Swift에서는 이에 해당하는 데이터 타입과 기능 대부분을 Swift 표준 라이브러리에서 제공한다.  
  
#### Foundation 기능별 요소
**기본**  
Number, Data, String: 원시 데이터 타입 사용  
Collection: Array, Dictionary, Set 등과 같은 컬렉션 타입 사용  
Date and Time: 날짜와 시간을 계산하거나 비교하는 작업  
Unit and Measurement: 물리적 차원을 숫자로 표현 및 관련 단위 간 변환 기능  
Data Formatting: 숫자, 날짜, 측정값 등을 문자열로 변환 또는 반대 작업  
Filter and Sorting: 컬렉션의 요소를 검사하거나 정렬하는 작업  
  
**애플리케이션 지원**  
Resources: 애플리케이션의 에셋과 번들 데이터에 접근 지원  
Notification: 정보를 퍼뜨리거나 받아들이기는 기능 지원  
App Extension: 확장 애플리케이션과의 상호작용 지원  
Error and Exceptions: API와의 상호작용에서 발생할 수 있는 문제 상황에 대처할 수 있는 기능 지원  
  
**파일 및 데이터 관리**  
File System: 파일 또는 폴더를 생성하고 읽고 쓰는 기능 관리  
Archives and Serialization: 속성 목록, JSON, 바이너리 파일들을 객체로 변환 또는 반대 작업 관리  
iCloud: 사용자의 iCloud 계정을 이용해 데이터를 동기화하는 작업 관리  
  
**네트워킹**  
URL Loading System: 표준 인터넷 프로토콜을 통해 URL과 상호작용하고 서버와 통신하는 작업  
Bonjour: 로컬 네트워크를 위한 작업  
​  
## CoreData
응용프로그램에서 모델 계층 개체를 관리하는 데 사용하는 Framework.  
지속성을 포함하여 객체 수명주기 및 객체 그래프 관리와 관련된 일반작업에 일반화되고 자동화 된 솔루션 제공한다.  
코어데이터는 구현, 테스트 또는 최적화 할 필요 없는 기본 제공 기능 때문에 모델 계층을 지원하기 위해 작성하는 코드의 양이 50–70% 감소한다.  
  
## MapKit​
앱의 인터페이스에 직접 지도 또는 위성이미지를 표시하고, 관심있는 장소를 호출하며 지도좌표에 대한 장소 표시 정보를 결정할 수 있는 도구모음입니다.  
  
## Core Animation
iOS 및 OS X에서 사용할 수 있는 그래픽 렌더링(Graphic Rendering : 컴퓨터 프로그램을 사용하여 그래픽으로부터 영상을 만들어내는 과정) 및 애니메이션 인프라(infrastructure : 기초적인 시설 및 자원) 로서 앱의 보기 및 시각적 요소에 애니메이션을 적용하는데 사용합니다.  
사용 시 애니메이션의 각 프레임을 그리는 데 필요한 대부분의 작업을 자동 수행합니다.  
  
---
**// AdLib Framework(광고 기능을 추가할 수 있는 프레임워크)**
