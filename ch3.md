## 앱 진입점
* 다트 프로그램처럼 플러터 앱도 main함수가 진입점
* 플러터에서는 runApp이라는 메서드로 최상위 위젯을 감싼다.

## 위젯
* 플러터에서 거의 모든 것이 위젯이며 위젯은 뷰를 묘사하는 다트 클래스다.
* 위젯은 요소를 화면에 표시할 때 플러터가 사용하는 청사진
* 위젯 클래스는 플러터가 이해할 수 있는 뷰 모델
* 위젯에는 컨트롤러나 뷰가 따로 없다.

## build 메서드
- 모든 위젯은 다른 위젯을 반환하는 build메서드를 반드시 포함해야한다.
```dart
class Redbutton extends StatelessWidget {
    Widget build(BuildCOntext context) {
        return new RaisedButton(
            // child elements
            //...
        )
    }
}
```

## 플러터의 new, const 생성자
* 플러터에서는 한 위젯의 여러 인스턴스를 만든다.
* 많은 내장 위젯은 일반 생성자와 const 생성자를 모두 제공한다.
* 변경할 수 없는 위젯 인스턴스는 성능이 좋으므로 가능하면 const를 사용하는 것이 좋다.
* new, const키워드를 둘다 사용하지 않으면 프레임워크가 가능한 const로 위젯을 추론하므로 크게 신경 쓰지 않아도 된댜.

## 핫리로드
* Intellij, VisualStudioCode, Android Studio에는 핫 리로드 전요 ㅇ버튼이 있으며 단축키는 cmd + s
* 터미널에서 플러터를 실행하고 r을 입력하면 실행

## 위젯트리 
* 플러터 UI를 개발한다는 것은 수많은 위젯을 조합해 위젯 트리를 완성함을 의미
* 브라우저에서 DOM으로 트리 구조를 표현하듯이 플러터 앱은 위젯 트리로 구현
* 각 노드는 위젯이고 노드가 모여 트리가 된다. build 메서드에서 위젯을 추가할 떄마다 트리에 새 노드를 추가한다.
* 각 노드는 부모와 자식관계로 연결된다.

## StatelessWidget
* 위젯 생명주기 동안 내부 상태를 갖지 않는다.
* 설정이나 자신이 표시하는 데이터를 신경 쓰지 않는다.
* 부모 위젯이 설정을 전달하거나 위젯 내부에서 설정 정보를 전달할 수 있지만 자신의 설정을 바꿀 수 없다.
* 상태를 바꿀 수 없는 위젯
```dart
[버튼 위젯 예제]
calss SubmitButton extends StatelessWidget {
    Widget build(context) {
        return Button(
            child: Text('submit'),
        );
    }
}

[설정을 포함하는 위젯]
class SubmitButton extends StatelessWidget {
    final String buttonText; // 위젯으로 전달한 모든 데이터를 설정으로 활용
    SubmitButton(this.buttonText); // 버튼의 텍스트로 설정할 데이터가 필요
    
    Widget build(context) {
        return Button(
            child: Text(buttonText), //  문자열 보다는 변수를 전달, 다른 변수를 전달하면 플러터가 이를 감지하고 버튼을 다시 그림
        );
    }
}
```

## StatefulWidget
* 상태를 갖는 모든 위젯은 State 객체를 갖는다.
* StatefulWidget클래스는 build 메서드를 포함하지 않는다. 대신 모든 StatefulWidget은 State 객체를 포함하며, 모든 State 객체는 build 메서드를 포함한다.
* StatefulWidget과 State는 같은 개체라고 생각해도 무방
* **StatefulWidget** 을 **StatelessWidget** 위젯처럼 변경할 수 없지만 `State객체는 변경할 수 있다`는 점을 이용하면 플러터가 위젯을 다시 그리는 동안에도 상태를 유지할 수 있다.
```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState(); // 모든 StatefulWidget은 State객체를 반환하는 createState메서드를 반드시 override
}

class _MyHomePageState extends State<MyHomePage> { // 상태 클래스는  플러터의 State클래스를 상속받는다.
  @override
  Widget build(BuildContext context) { // StatefulWidget의 필수 build메서드
      //...
  }
}
```

## `_`로 시작하는 다트의 비공개 값
* 클래스 이름을 언더바(_)로 시작하면 **private** 클래스를 의미
* 모든 행을 private으로 설정할 수 있따.
* 클래스처럼 최상위 수준의 값을 현재 파일에서만 이용하려면 private으로 설정한다.
* 변수나 함수처럼 클래스 멤버를 private으로 설정하면 현재 클래스에서만 이를 접근할 수 있다.
```dart
class Cat {
    String name;
    String _color;
    void meow() => print("meow");
    void_pur() => print("prrr");
}

void main() {
    Cat nora = Cat();
    nora.name = "Nora"; //valid
    nora._color = "Orange"; //invalid
    nora.meow(); //valid
    nora._pur(); //invalid
}
```

## setState
* **build** , **createState** 다음으로 중요한 메서드
* 객체의 상태와 관련이 있다.
* 이 메서드는 **Void-Callback** 형식의 인수 하나를 갖는다.
* setState를 호출하면 build메서드를 실행하면서 설정이 바뀐 모든 위젯을 다시 그린다.
* `비동기 코드를 실행할 수 없다`는 점에 주의
* 플러터가 위젯을 다시 그릴 때 필요한 데이터가 준비되어 있어야 하기 때문에, setState를 실행하기 전에 모든 비동기 코드를 완료해야 한다.


## initState
* State 객체는 위젯이 트리에 마운트 되면 호출되는 iniState 메드도 포함
* 플러터가 화면에 위젯을 그리기 전에 필요한 모든 초기화를 State.iniState 메서드에서 수행
* 플러터가 StatefulWidget과 State 객체를 만들 때 가장 먼저 initState함수를 실행

```dart
class FirtNameTextState extends State<FirstNameText> {
    String name;

    FirstNameSTextState(this.name);

    @override
    initState() {
        super.initState(); // 반드시 슈퍼클래스 구현을 호출행야 한다.
        name = name.toUpperCase();
    }
}
```

* initState메서드는 State객체를 만들 때 한번 호출되고, setState로 위젯 갱신

## BuildContext
* 앱을 만들 때 알아야 할 중요한 개념중 하나로 전체 위젯 트리를 추적하는 것과 관련이 있으며 특히 트리에서 위젯의 위치와 관련이 있다.
* 위젯의 모든 build 메서드는 위젯 트리에서 위젯의 위치를 참조하는 BuildContext 하나를 인수로 받는다. build는 프레임워크가 호출하므로 BuildCOntext를 개발자가 관리할 필요는 없지만 자주 이를 사용하게 된다.
* 모든 위젯은 자신만의 BuildContext를 가지며 한 위젯이 다양한 테마를 반환하게 만들어 한 트리에 여러 테마를 적용할 수 있다.
카운터 앱의 테마나 다른 `of` 메서드는  트리에서 형식이 같은 가장 가까운 부모를 반환\
* 특정 위젯을 정확하게 어떻게 표현할지 결정
* 위젯 자체의 정보가 아니라 위젯 트리에서 위젯의 위치 정보를 포함

## 기본적인 위젯 목록
* Container
* Row
* Column
* Image
* Text
* Icon
* RaisedButton
* Scaffold
* AppBar

## RaisedButton
* material 디자인에서 제공하는 버튼중 하나로 elevated 효과를 제공
* This class is deprecated, please use [ElevatedButton] instead.
* 플러터에서는 onPressed와 같은 콜백으로 상호작응 처리
* 플러터에서 제공하거나 또는 직접 만든 위젯은 콜백을 통해 사용자와 상호작하며 지정된 함수를 실행
* 내장 위젯은 onPressed, onTapped, onHorizontalDrag등 다양한 콜백을 갖는다.

## 상속보다 조합을 선호하는 플러터
> 객체지향 소프트웨어 설계는 어렵다. 하지만 재사용할 수 있는 객체지향 솦트웨어를 설계하는 것은 더 어렵다.
* 객체지향 프로그래밍ㅇ에서 클래스 관계를 정의하기란 가장 어려운 설계 문제중 하나다.
* 클래스 관계는 보통 두가지 방법 중 하나로 연결한다.  
  - 상속: is - a 관계 (~은(는) ~이다.)
  - 조합: has a 관계(갖고 있다.) 
* 보통 객체의 실체를 설계할 때 상속을 선택하고, 객체의 기능을 설계할 때 조합을 선택
```dart
class PanicButton extends StatelessWidget {
    final Widget display;
    final VoiceCallback onPressed;

    PanicButton({this.display, this.onPressed}); // 표현할 위젯(Text("Panic")같은)과 위젯 설정을 전달.

    Widget build(BuildContext context) {
        return RaisedButton(
            color: Colors.red, // 버튼의 배경을 빨간색으로 설정
            child: display, // 부모가 텍스트 위젯을 전달(이게 핵심)
            onPressed: onPressed, //콜백도 전달, 콜백의 내용을 알필요가 없으며 부모에 전달(콜백을 통해)하는 일만 담당
        )
    }
}
```

## 레이아웃
* 플러터 렌더링 엔진은 한 가지 정해진 레이아웃 시스템을 사용하지 않는다는점이 독특

## Row와 Column
* 플러터에서는 웹의 FlexBox와 비슷한 Flexible 레이아웃이 가장 흔하다.
* Column, Row위젯으로 Flexible 레이아웃을 사용
* Row: 수평(Horizontal)
* Column: 수직(vertical)

## RenderObject
* 이 클래스는 내부에서 사용되는 클래스이므로 플러터 앱 개발자가 이를 직접사용하는 일은 드물다.
* 실제 화면에 그리는 작업을 담당
* 프레임워크 내부에서 이 클래스를 구현하며 모든 RenderObject가 모여 Render Tree를 만든다.
* RenderTree는 RederObject를 구현하는 클래스로 구성되며 렌더 객체느 각자 대응하는 위젯을 갖는다.
* 개발자는 RederObject에 제약조건같은 데이터를 제공
* performLayout, paint 같은 메서드를 제공
* 상태나 로직을 포함하지 않는다.
위젯은 build메서드에서 자식 메서드를 만들 수 있으므로 트리의 가장 아래에 내려가야 RenderObjectWidget을 찾을 수 있다. 
* RenderObjectWidget은 화면을 그리는 RenderObject를 만드는 위젯

## RenderObject와 제약 조건
* 제약조건은 minWidth, minHeight, maxWidth, maxHeight 등의 프로퍼티로 설정
* RenderBox는 아주 흔한 RenderObject의 서브클래스로 데카르트 좌표계를 기반으로 위젯크기를 계산
* RenderBox
  - Center Widget: 최대 공간 차지
  - Opacity Widget: 자식과 같은 크기의 공간 차지
  - Image Widget: 특정 크기의 공간 차지

## RenderBox와 레이아웃 오류
- flutter layout infinite size오류: 위젯이 수평, 수직으로 무한 크기를 갖도록 제약 조건이 설정되었을 떄 발생  
-> RenderObject가 전달된 제약조건을 처리하는 과정에서 발생
* RenderBox에 한정되지 않은(unbounded) 제약조건을 제공할 수 있다. maxHeight나 maxWidght를 제공하면 renderBox는 double.INFINITY값을 갖는다.  
특히 Row, Column, 스크롤할 수 있는 위젯에서 한정되지 않은 제약조건을 자주 사용한다.  
Row, Column은 특별한 플렉스 상자다. 부모가 한정된 제약 조건을 가지면 이들은 `한정된 제약조건 내에서` 최대한의 공간을 차지한다.
  - Row: 부모만큼의 높이를 가진다.
  - Column: 부모만큼의 너비를 가진다.

## Image
* 앱에 이미지를 쉽게 추가
* 이미지소스(로컬, 인터넷 등)에 따라 다양한 생성자를 제공
* `Image.network` 생성자를 이용해 URL을 문자열로 제공하면 모든것을 알아서 처리
  - 예) Image.network("https://funfreegifs.com/panda-bear")
* `Image.asset` 생성자를 이용해 프로젝트 상의 이미지 경로를 전달하면 로컬 이미지를 사용, 하지만 로컬 이미지를 사용하려면 먼저 pubspec.yaml파일에 이미지 위치를 선언해야한다.
* 앱에서 사용하는 모든 asset을 pubspec.yaml 파일의 assets헤더에 추가, YAML 은 공백을 인식하므로 주의
```yaml
flutter:
    uses-material-design: true
    asssets:
      - ...
```
* lib 폴더에 추가한 파일은 lib폴더를 기준으로 경로를 지정 
  - 예) lib/iamges폴더에 이미 저장한경우: images/xxxx.png
  * pubspec.yaml파일을 바꾸었을 때는 핫 리로드가 적용되지 않지만 핫 재시작은 정상 동작한다. 핫 재시작 기능을 이용하면 앱을 멈췄다 재시작 하는것보다 빨리 앱을 실행한다.

  ## 위젯 키
  * 상태와 요소 문제는 키로 쉽게 해결할 수 있다.
  * 여러 위젯이 있을 때 키를 이요하면, 두 위젯의 형식은 같지만 다른 위젯임을 플러터에 알릴 수 있따.
  * 특히 여러 자식을 갖는 위젯에서 유용하게 활용

  ## 키의 형식과 사용 방법
  * ValueKey, ObjectKey, UniqueKey, GlobalKey, PageStorageKey 등 여러 종류의 키가 있으며 서로 공통된 부분이 있다.
  예를 들어 PageStorageKey는 ValueKey<T>를 상속받으며 ValueKey<T>는 LocalKey를 상속받고 LocalKey는 Key를 상속받는다. 
  ObjectKey와 UniqueKey도 LocalKey를 구현한다. GlobalKey는 Key를 상속받는다. 이렇게 모두 Key형식을 갖는다.
  
## 글로벌 키
* 위젯트리에서 상태를 관리하고 위젯을 이동할 때 클로벌 키를 사용
* 글로벌 키는 프레임워크에 같은 위젯이 여러 곳에 사용되었음을 알린다.
* 이때 다양한 페이지에 위치한 체크박스는 같은 checked상태를 공유한다. A라는 페이지에서 체크박스를 체크했다면 B라는 페이지의 체크박스도 체크되어 있다.
* 글로벌 키로 상태를 관리하는 것을 권장하지 안흔다.(플러터 팀의 권고 사항)
* 글로벌 키는 성능에 영향을 미치므로 자주 사용하지 않으며 로컬 키를 주로 사용한다.

## 로컬 키
* 로컬 키는 키를 생성한 BuildContext의 영역을 갖는다. 
  - ValueKey<T>: 상수를 갖는 객체에 키를 추가할 때 ValueKey를 사용한다. 예를 들어 할 일 목록 앱에서 할일을 표시하는 위젯은 고유한 상수 Todo.text를 포함한다.
  - ObjectKey: 같은 형식의 객체지만 프로퍼티 값이 다른 여러 객체가 있을 때 ObjectKey를 사용한다. product라는 전자상거래 앱이 있다고 가정하자. 두 제품의 이름이 같을 수 있다(두 판매자가 같은 이름의 상품을 파는상황). 그리고 한 판매자가 여러 제품을 판다면 제품명과 판매자명을 조합해 특정 제품을 식별할 수 있다. 즉 ObjectKey로 전달하는 literal 객체가 키다
  ```dart
  Key key = ObjectKey({
      "seller": product.seller,
      "product": product.title
  })
  ```
  - UniqueKey: 컬렉션에 자식이 있고 이들이 만들어지기 전까지 자식의 값을 모르는 상황이라면 UniqueKey를 자식에 추가한다. 예제 앱에서 제품 카드를 다시 만들기 전까지는 색을 모르므로 UniqueKey를 이용할 수 있다.
  - PageStorageKey:스크롤 위치 등 페이지 정보를 저장하는 특수 키다.

  ## 정리
* 플러터의 모든 것은 위젯이며 위젯은 뷰를 묘사하는 다트 클래스다.
* 위젯은 앱 뷰의 모든 정보를 정의할 수 있다. Row 같은 위젯은 레이아웃을 정의한다. 어떤 위젯은 추상화가 덜되어있으며 Button, TextField처럼 구조적 요소를 정의한다.
* 플러터는 상속보다 조합을 중시한다. 조합은 `has a`관계를, 상속은 `is a`관계를 정의한다.
* 모든 위젯은 위젯을 반환하는 build 메서드를 포함해야 한다.
* 플러터에서 위젯은 변경할 수 없지만 상태 객체는 바꿀 수 있다.
* 위젯은 대부분 const 생성자를 갖는다. 플러터에서 위젯을 만들 때 new와 const 키워드는 생략하는 것이 좋다.
* StatefulWidget은 상태 객체로 자신의 내부 상태를 관리한다. StatelessWidget은 `뇌가 없으며(dumb)` 플러터가 위젯 트리에서 위젯을 제거하면 완전히 파괴된다.
* setState는 플러터에 상태를 갱신하고 위젯을 다시 그리도록 지시한다. setState에서는 비동기 작업을 수행하지 않아야 한다.
* initState와 기타 생명주기 메서드는 상태 객체의 강력한 도구다.
* BuildContext는 위젯 트리에서 위치를 가리킨다. 즉 위젯은 트리에서 자신의 위치 정보를 얻을 수 있다.
* 요소 트리는 영리하다. 요소 트리는 위젯을 관리하며 실제 사용될 요소의 청사진 역할을 한다.
* 플러터에서 위젯과 관련된 RenderBox 객체가 위젯을 그린다. 이들 RenderBox는 위젯의 실제 물리적 크기를 결정한다. 이들 객체는 부모로부터 제약 조건을 받아 자신의 실제 크기를 결정한다.
* Container 위젯은 개별위젯에서 얻어야 할 정보를 '편리하게' 모아 제공한다.
* 플러터의 Row, Column 위젯은 CSS의 FlexBox와 비슷한 플렉스 레이아웃 개념을 사용한다.
