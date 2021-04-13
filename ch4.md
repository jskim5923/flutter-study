## SystemChrome
* 네이티브 플랫폼에서 앱이 표시되는 방법을 제어하는 플러터 클래스
* 디바이스를 제어하는 데 사용하는 유일한 클래스(플러그인을 개발하지 않는다는 조건)

## Future
* 다트의 모든 비동기 프로그래밍의 기초를 구성하는 클래스
* Future.then은 나중에 값을 구했을 때 실행할 콜백을 받는다.

## MaterialApp 위젯
* 전체 위젯 서브트리에 적용되는 다양한 기능을 제공
* 플러터에서 제공하는 최상위 수준의 위젯 WidgetsApp을 상속 받는다
* WidgetsApp은 네비게이션 설정, 앱 전반의 테마 사용 등 대부분의 모바일 앱에 필요한 기능을 추상화해 제공하는 편리한 위젯
* WidgetsApp은 기본설정, 스타일 혹은 앱 UI구조 등을 제한하지 않으므로 자유롭게 이를 커스터마이즈할 수 있다.

## Scaffold 위젯
* MaterialApp 위젯은 앱의 설정과 기능을 제공
* Scaffold 위젯은 앱 구조를 만드는 일을 돕는다.
* MaterialApp이 앱의 배관, 전기라면 Scaffold는 뼈대와 벽이라 할 수 있다.
* drawer, bottom sheet 등을 추가 하는 ㅈ기능을 제공
* 따로 설정하지 않으면 Scaffold의 AppBar는 앱 왼쪽 윗부분에 메뉴 버튼을 기본으로 표시하며 이 버튼을 누르면 드로어가 열린다.
* 메뉴를 포함하지 않는 화면에서는 메뉴 버튼 대신 back 버튼이 나타난다.
* 이들 버튼의 동작은 모두 완성된 상태로 제공되고, 예상하는 대로 동작한다.
* 하지만 직접 필요한 기능과 필요하지지 않은 기능을 선택할 수 있다. 앱에 drawer 스타일 메뉴를 사용하지 않을 때는 drawer를 전달하지 않으면 메뉴 버튼도 사라진다.


## AppBar 위젯
* 보통 Scaffold.appbar 프로퍼티에 사용하며 화면 위쪽에 특정 높이의 공간을 차지
* 대표적인 기능은 네이게이션 부모가 Scaffold이고 drawer인수가 null이 아니라면 자동으로 메뉴 버튼을 추가 '뒤로'갈 수 있는 화면이라고 판단되면 앱의 Navigator는 자동으로 백 버튼을 추가
* 중요한 프로퍼티
  - 메뉴 버튼과 back 버튼을 처리하는 프로퍼티를 리딩액션(leading action)이라 부르며, AppBar.leading, Appbar.automaticallyImplyLeading 프로퍼티로 설정할 수 있다.
    - AppBar.automaticallyImplyLeading을 false로 설정하고 leading 인수를 다른 위젯으로 전달하면 해당 위젯이 AppBar의 가장 왼쪽에 위치한다.

## PrefferedSize 위젯
* 플러터에서 위젯의 크기는 부모의 제약을 받는다.
* 위젯은 제약 조건 정보를 획득한 다음 최종 크기를 결정한다.
* 부모가 전달한 제약조건은 위젯이 얼마나 큰 공간을 차지할 수 있는지 알려주지만 최종 크기에 직접 과여하진 앟ㄴ는다.
* 이 시스템의 장점은 유연성이다.
* 명시적으로 너비와 높이를 설정할 수 있다.

## Theme 위젯
* 앱 전체에 스타일을 적용
* 스타일이 적용되지 않는 상황 또는 기존 스타일을 오버라이드해야 하는 상황이라면 위젯 트리 어디에서나 Theme 위젯에 접근하여 해결할 수 있다.
* 다양한 색 관련 프로퍼티(앱 전체 위젯에 영항)
  - brightness(어두운 테마나 밝은 테마로 설정)
  - primarySwatch
  - primaryColor
  - accentColor
* 특정 기능을 제어하는 프로퍼티
  - canvasColor
  - scaffoldBackgroundColor
  - dividerColor
  - cardColor
  - buttonColor
  - errorColor
* 기본 폰트, 애니메이션, 아이콘 스타일 등을 설정하는 20개가 넘는 인수가 있다. 인수 중 일부(내부에 프로퍼티를 갖는 클래스)는 앱을 다양하게 커스터마이즈할 수 있다.

## 앱에 테마 설정하기
* ThemeData를 이용해 테마를 설정
* MaterialApp.theme 프로퍼티에 ThemeData 객체를 전달해 테마르 ㄹ추가
* 직접 Theme 위젯을 만들어 ThemeData객체에 전달
* Theme은 위젯이므로 다른 위젯처럼 어디에나 사용할 수 있다.
* 모든 위젯의 theme 프로퍼티는 위젯 트리의 가장 가까운 곳에서 상속받은 Theme 위젯을 사용  
-> 앱의 최상위 수준의 테마를 오버라이드하는 여러 테마를 만들 수 있다.
* BuildContext로 앱의 어디서나 ThemeData를 얻을 수 있다.

## MediaQuery와 of메서드
* 플러터에서는 논리적 픽셀(logical pixel) 한 가지 단위만 사용
* 대부분의 레이아웃 크기 문제를 수학으로 해결해야 하는데 화면의 크기에 따라 계산 결과가 달라진다.
* 플러터에서는 퍼센트를 사용할 수 없으므로 MediaQuery 위젯을 이용해 화면 크기르 먼저 알아내야 한다.
* Theme처럼 BuildContext를 이용해 앱 어디서든 MediaQuery 위젯을 사용할 수 있다. 
* of메서드는 트리에서 가장 가까운 MediaQuery 클래스의 레퍼런스를 반환한다.
* MediaQuery.of(context).size 메서드는 디바이스의 너비나 높이 정보를 포함하는 Size 객체를 반환한다.
* of는 static 메서드이므로 MediaQuery 클래스의 인스턴스를 만들지 않고 직접 호출한다.
* of 메서드는 호출한 BuildContext를 알고 있는 MediaQuery 클래스의 레퍼런스를 반환한다.
```dart
[화면의 80%로 위젯의 너비를 설정하는 코드]
final width = MediaQuery.of(context).size.width * 0.8;
```
* MediaQuery를 활용하는 경우
  - 휴대폰의 가로/세로 방향 확인
  - 접근성과 관련해 애니메이션을 비활성화하고 색을 반전시킬 경우
  - 사용자가 텍스트 크기를 확대했는지 확인할 경우
  - 전체 앱에 패딩을 설정하 경우

## Stack 위젯
* 한 위젯 위에 다른 위젯을 쌓아 올릴 때 사용
* 스택의 API를 이용해 화면의 스택 경계에서 정확히 어떤 위치에 위젯을 추가할지 설정한다.  
(CSS의 positon:fixed와 비슷)
* 스택은 자식의 위치를 지정하거나 지정하지 않을 수 있다.(기본값)
* 위치를 지정하지 않은 자식을 Column이나 Row가 자식을 취급한는 것처럼 처리한다.  
-> 자식 위젯을 왼쪽 위 모서리로 정렬하며 이들을 나란히 놓는다.
* alignment 프로퍼티로 정렬 방향을 설정한다.  
-> 자식의 위치를 명시적으로 지정하지 않으면 스택은 자식들을 수직으로 배치한다.
* 위치를 지정한 위젯은 top, left, right, bottom, widght, height 등의 프로퍼티를 갖는다. 보통 이들 중 최대 두개의 수평 프로퍼티(left, right, width)와 두 개의 수직 프로퍼티(top, bottom, height)를 설정한다. 이 프로퍼티로 위젯을 그릴 위치를 설정하면 RenderStack 알고리즘이 자식을 그린다.
* 모든 위젯의 배치를 마쳤으 스택의 `바닥`에 위치한 위젯부터 차례대로 그린다


## Table 위젯
* Table은 위젯을 행과 열로 배치
* 표의 각 셀은 같은 행의 다른 셀과 같은 높이를 가지며, 같은 열의 다른 셀과 같은 너비를 갖는다.
* 빈 Table 셀은 존재할 수 없으므로 Table을 만들 때 열의 너비를 명시적으로 설정해야 한다.
* 기억해야할 내용
  - columnWidths는 전달할 필요가 없지만 defaultColumnWidth는 null로 설정할 수 없다.
  - defaultColumnWidth는 기본 인숫값으로 FlexColumnWidth(1.0)을 가지므로 아무 값도 전달하지 않아도 괜찮지만 null로 설정할 순 없다. defaultColumnWidth null로 설정하면 오류가 발생한다. defaultColumnWidth는 기본값을 가지므로 따로 값을 설정하지 않으면 모든 셀이 같은 너비를 가지며 Table은 가능한 큰 공간을 차지한다.
  - columnWidths로 열의 너비를 설정한다. Map은 열의 인덱스와 열의 너비를 키로 갖는다.
  - children 인수는 List<TableRow>를 기대하므로 아무 위젯이나 전달할 수 없다. 지금까지 이런 상황은 없었지만 조금 더 복잡한 위젯을 다루다 보면 이런 상황을 종종 겪는다.
  - Border는 선택형이다.
  - 행의 자식이 TableCell이어야 TableCellVerticalAlignment가 동작한다.
  * Table에 자식만 전달하면 모든 열은 같은 너비를 갖는다.
  * 행의 요소는 전체 너비를 최대한 활용한다.
  * TableRow
    - Table의 모든 행은 같은 수의 자식을 가져야 한다.
    - 자식의 버스 위젯 트리에 TableCell을 반드시 사용할 필요는 없다. TableCell은 TableRow의 직계자식이어야 할 필요는 없으며 위젯 트리의 어딘가에 TableRow를 조상으로 가지면 충분하다.
* 요점
  - 탭을 구현하려면 TabController와 자식 위젯이 필요하다. 자식을 탭하면 관련 내용을 화면에 표시한다.
  - 탭 바의 위젯을 탭하면 콜백을 통해 탭을 전환할 수 있다. 콜백은 TabController가 제공하는 프로퍼티를 사용해 플러터에 새 탭을 그리도록 지시한다.


## TabBar위젯
* 자식들을 스크롤할 수 있고, 수평의 뷰로 구성되며 tappable 기능을 갖는다.
* 탭하면 탭바 위젯에 전달한 콜백이 호출되며, 이 콜백을 이용해 TabBar의 자식 위젯은 페이지의 위젯을 바꾼다.
* TabBar위젯은 자식(사용자가 선택할 수 있도록 표시하는 위젯)과 필요한 기능을 처리하는 TabController 두가지 핵심 기능을 제공

## TabController 위젯
* 플러터에서 많은 대화형 위젯은 이벤트를 관리할 수 있도록 관련 컨트롤러를 갖는다.
* 사용자가 새 탭을 선택했을 때 앱이 필요한 컨텐츠를 갱신하도록 알리는 역할을 담당한다.
* 리스너 뿐만 아니라 탭과 관련 contents를 관리하도록 돕는 getter를 갖는다.


## 리스너
* 비동기 기능을 실행할 때 활용하는 기법일 뿐 특별한 객체거나 다른 형식을 갖지 않는다.
* 플러터 라이브러리에서 리느터 change notifier, stream 등의 용어를 자주 접하게 된다. 이들은 모두 observable이라는 같은 종류의 프로그래밍 컨셉을 구현한다.


## ListView와 빌더
* 자주 사용할 뿐만 아니라 효과적인 플러터 앱을 구현하는 데 필요한 패턴과 개념을 포함
* ListView의 기본생성자에서 플러터는 모든 자식을 한번에 빌드하고 그린다.
* ListView.builder 생성자는 itemBuilder 프로퍼티로 콜백을 받으며 이 콜백을 통해 위젯을 반환한다.
* 특히 리스트에 표시해야 할 항목의 수가 아주 많거나 무한대라면 플러터는 빌더 덕분에 효과적으로 화면에 항목을 그릴 수 있다.
* 플러터는 사용자가 뷰에서 스크롤할 때 필요한 항목만 그린다.
* 다양한 생성자
  - ListView.separated는 ListView.builder와 비슷하지만 두 가지 빌더 메서드를 받는다. 한 가지는 리스트 항목을 만들 때 사용하고 나머지 한가지는 리스트 항목 간의 분리자를 만드는 데 사용한다.
  - ListView.custom을 이용하면 커스텀 자식으로 리스트 뷰를 만든다. 다만 빌더처럼 간단하지는 않다. 리스트 뷰의 항목을 각자 다른 항목으로 만들어야 한다고 가정하자. 이럴 때 Custom ListView를 사용한다. Custom ListView를 이용하면 자식을 어떻게 그려야 할지를 잘 제어할 수 있기 때문에다. 

## 정리
* 플러터는 MaterialApp, Scaffold, AppBar 등 다양한고 편리한 기능을 가진, 구조를 만들 수 있는 위젯을 제공한다. 위젯을 이용하면 Navigation,Menu  Drawer, Theme등의 기능을 공짜로 누릴 수 있다.
* SystemChrome 클래스로 앱을 가로 또는 세로모드로 설정하는 등의 디바이스 기능을 사용한다.
* MediaQuery를 이용해 화면 크기 정보를 얻는다. 특히 화면 크기에 따라 위젯의 크기를 조절할 때 유용하다.
* Theme으로 스타일 프로퍼티를 설정하면 앱 전체 위젯에 영향을 준다.
* Stack 위젯으로 화면의 위젯을 원하는 위치에 쌓는다.
* Table 위젯으로 표 형식의 위젯을 배치한다.
* ListView와 빌더를 이용하면 간단하게 무한대의 항목을 가진 리스트를 만들 수 있고 동시에 빠른 성능도 보장한다.