## 다트의 프로그래밍 개념
* 다트는 객체지향 언어이며 단일 상속(single inheritance)을 지원한다.
* 다트에서 모든 것이 객체이며 모든 객체는 클래스의 인스턴스다. 모든 객체는 Object 클래스를 상속받는다.
* 다트는 type을 갖는다. 
* 다트는 최상위 수준 함수와 변수를 지원하며 이를 라이브러리 멤버(library member)라 부른다.
* 다트는 어휘적(exically)으로 한정된다.

## 동적 형식
* 다트는 동적 형식(dynamic type)도 지원한다. 변수를 `dynamic` 으로 설정하면 컴파일러가 해당 변수에 `모든` 형식을 허용한다.
```dart
dynamic myNumber = 'Hello';
```
모든 변수 형식에 `dynamic` 을 설정하면 결과적으로 다트를 `선택적 형식(optionally typed)` 으로 바꾼다. 하지만 형식을 사용하면서 얻는 이득이 사라질 뿐 아니라 모든 변수에 `dynamic` 이라는 키워드를 사용해야한다.

```dart
var myString = 'Hello';
myString = 3 // 컴파일러 오류
```
변수의 형식을 한번 결정하면 이를 바꿀 수 없다. 

```dart
myPrint() { // 함수의 반환 형식이 없다.
    print('hello');
}
```

위와 같이 컴파일러가 함수의 형식을 자동으로 출론 하기 때문에 함수도 반환 형식을 생략할 수 있다.

## 동적 형식(dynamic)이 유용하게 사용 되는 경우
* 보통 맵에 dynamic을 사용한다. 
```dart
Map<String, dynamic> json; //JSON을 처리하는 변수
```
JSON을 다트 객체로 변환할 때 맵의 키는 String이라는 사실을 알지만 값은 String, int, List, 다른 Map이 될 수도 있다. var 키워드는 코드 형식에 도움을 주는 키워드다. `dynamic` 과 달리 변수를 정의할 때만 var를 사용할 수 있으며 형식에는 사용할 수 없다. 
```dart
Map<String, var> json; // 잘못된 var 사용!
```

var를 사용할 수 있는 범위는 한정적이다. var를 사용할 수 있는 상황이라 하더라도 가능하면 변수의 실제 형식을 사용하는 것이 좋다. 변수에 다시 값을 사용할 수 없으면 `final` 을 사용한다.(다른 형식 정의 없이). 보통 `final`은 클래스 멤버가 아닌 함수 바디에 사용한다. 그 밖의 상황에서는 형식을 사용하는 것이 좋다.

## 변수와 할당
* 다트에서는 할당하지 않은 변수를 null로 초기화 한다.
* 다트에서는 null도 객체다.
* 따라서 int, String, List 등 모든 것에 null을 할당할 수 있다.
* [다트 스타일 가이드](https://dart.dev/guides/language/effective-dart/usage#dont-explicitly-initialize-variables-to-null)에 따르면 객체에 null을 명시적으로 할당하지 않는 것이 좋다.

## final, static
* final과 const 모두 상수화 시킨다
  - final은 실행 단계에서 값이 대입되고,
  - const는 컴파일 단계에서 값이 대입된다.
* `const` 를 사용하면 성능이 개선되므로 가능한 곳에는 const를 사용하는 것이 좋다. 플러터는 클래스와 위젯을 const로 만드는 특별한 도구를 제공한다.


 ## Null-Safety
 * ?.: kotlin의 `?.`연산자와 동일
 * ??: kotlin의 `?:`연산자와 동일
 * ??=: 객체가 null이면 백업 값을 할당하고 아니면 객체를 그대로 반환한다.
 ```dart
 int x = 5;
 x ??= 3; // x는 값을 가지므로 3이 할당 된다.
 ```

 ## switch-case
 * 각 case block에 break/return 등 탈출 키워드를 넣지 않으면 오류가 발생
 ```dart
 switch(number) {
     case 1:
     print(number);
     // 오류 !
     case 2: 
      //...
 }
 ```
## 함수
* 다트는 한 표현식을 포함하는 함수에 적용할 수 있는 단축 표현도 제공한다. 
```dart
String makeGreeting(String name) => 'Hello, $name';
```

* 화살표 함수(arrow function)
  - `=> 표현식;`의 문법으로 결과를 반환 이는 {return 표현식;} 코드와 동일
  - 화살표 함수에서는 `return`키워드를 사용할 필요가 없다.

## 파라미터
* 이름 지정 파라미터(named parameter)
  - 함수를 호출할 때 인수를 레이블과 쌍으로 제공한다는 의미
  - 중괄호로 이름 지정 파라미터를 감싸서 이름 지정 파라미터를 구현  
    기본적으로 일므 지정 파라미터는 선택사항
```dart
debugger(message: 'A bug!', lineNumb: 44);

void debugger({required String message, required int lineNum}) {...}
``` 

* 선택형 위치 지정 파라미터
  - 마지막으로 []를 이용해 정의

```dart
[정의]
int addSomeNums(int x, int y, [int z]) {
    int sum = x + y;
    if( z != null) {
        sum += z;
    }
    return z;
 }

[호출]
addSomeNums(5,4) // 세 번째 파라미터는 선택형이므로 인수를 전달하지 않아도 괜찮다.
addSomeNums(5, 4, 3) // 세 번째 파라미터는 선택형이므로 인수를 전달할 수 있다.
```

* 파라미터 기본값
  - 함수 시그니처에 = 연산자를 이용해 파라미터의 기본값을 정의
```dart
 addSomeNums(int x, int y, [int z = 5]) => x + y + z;
```
  

## new 키워드
* 다른 객체지향 언어에서는 new 키워드로 클래스와 인스턴스를 만든다. 다트에서도  `new`를 사용할 수 있지만 이는 선택 사항이다.
* 다트 2에서는 `new`나 `const`로 객체를 만들 필요가 없다. 컴파일러가 자동으로 알맞은 키워드를 추론하기 때문이다. 
* 다트에서는 `new` 키워드 사용을 권장하지 않는다.

## 생성자
* 일부 언어에서는 생성자 바디에서 각 프로퍼티 변수를 명시적으로 할당해야 하지만, 다트에서는 더 간결하게 줄일 수 있다.
```dart
class Animal {
    String name, type;

    Animal(this.name, this.type);
}
```

## factory, 지정 생성자
* 지정 생성자: 항상 클래스의 `새 인스턴스를`반환
* factory: 캐시된 인스턴스 또는 서브 형식의 인스턴스를 반환(싱글톤)
```dart
class Energy {
    int joules;

    Energy(this.joules); // 기본 생성자

    Energy.fromWind(int windBlows) { // 지정 생성자는 'Energy.'문법을 이용해 클래스의 인스턴스를 반환
        final joules = _convertWindToEnergy(windBlows);
        return Energy(joules); // 모든 생성자는 클래스의 인스턴스를 반환해야 한다.
    }

    factory Energy.fromSolar(int sunbeams) {  // factory는 기존 Energy 인스턴스를 반환할 수 있다. 또는 새 인스턴스를 만들어 할당한 다음 반환
        if (appState.solarEnergy != null) return appState.solarEnergy;
        final joules = _convertSunbeamsToJoules(sunbeams);
        return appState.solarEnergy = Energy(joules);
    }
}
```

## 정리
* 다트 문법은 C언어를 기반으로 만들어진 언어와 비슷하다.
* 다트는 객체지향이며 엄격한 형식 언어다.
* 모든 다틐 프로그램의 진입점은 main 함수다.
* 형식은 특정 상황에 올바른 값을 할당하도록 코드를 강제한다. 때로는 귀찮아 보일 수 있지만 버그를 줄이는 데 도움이 된다.
* 함수는 형식 또는 void를 반환해야 한다.
* 다트의 대부분의 연산자는 다른 연산자와 비슷하지만 ~/, is, as처럼 특별한 연산자도 있다.
* 어떤 값이 null이 아닌지 확인할 때 널 인지 연산자를 활용한다.
* 다트는 if/else, switch, 삼항 연산자 등의 제어 흐름을 제공한다.
* switch 문에 enum을 사용하면 모든 enu의 형식을 case로 확인하도록 컴파일러가 강제한다.
* 다트의 루프는 다른 언어와 비슷하다. 다트는 for, for-in, while, do while루프를 지원한다.
* 다트의 함수는 객체이므로 값처럼 함수를 전달할 수 있다. 다른 언어에서는 이름 `고차함수`라 부른다.
* 다트는 진정한 객체지향 프로그래밍 언어이므로 여러분은 클래스, 생성자, 상속을 자주 사용할 것이다.
* 다트는 기본 생성자, factory 생성자, 지정 생성자 등 다양한 생성자를 지원한다.
* enum은 프로퍼티나 변수에 정해진 범위의 형식을 지정하므로 형식 안정성을 제공하는 특별한 클래스다. 