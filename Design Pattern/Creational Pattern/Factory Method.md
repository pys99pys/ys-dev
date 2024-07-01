# Factory Method

https://refactoring.guru/design-patterns/factory-method 를 공부하며 정리한 내용입니다.

## Factory Method란?

Factory Method는 슈퍼클래스에서 객체를 생성하기 위한 인터페이스를 제공하지만 서브클래스가 생성될 객체의 유형을 변경할 수 있도록 하는 생성 디자인 패턴입니다.

![alt](./images/Factory%20Method1.png)

## 문제

물류 관리 응용 프로그램을 만들고 있다고 상상해보십시오. 앱의 첫 번째 버전은 트럭으로만 운송할 수 있으므로 대부분의 코드는 Truck 클래스 내에 있습니다.

잠시 후 앱이 꽤 유명해집니다. 매일 해상 운송 회사로부터 해상 물류를 앱에 통합해 달라는 수십 개의 요청을 받습니다.

![alt](./images/Factory%20Method2.png)

_<코드의 나머지 부분이 이미 기존 클래스에 연결되어 있는 경우 프로그램에 새 클래스를 추가하는 것은 그리 간단하지 않습니다.>_

좋은 소식이죠? 하지만 코드는 어떻습니까? 현재 대부분의 코드는 Truck 클래스에 연결되어 있습니다. 앱에 Ships를 추가하려면 전체 코드베이스를 변경해야 합니다. 또한 나중에 앱에 다른 유형의 교통 수단을 추가하기로 결정한 경우 이러한 모든 변경을 다시 수행해야 할 수도 있습니다.

결과적으로 운송 객체의 클래스에 따라 앱의 동작을 전환하는 조건부로 가득 찬 꽤 불쾌한 코드로 끝납니다.

## 해결책

Factory Method 패턴은 직접적인 객체 생성 호출(new 연산자 사용)을 특별한 Factory Method에 대한 호출로 대체할 것을 제안합니다. 걱정하지 마십시오. 객체는 여전히 new 연산자를 통해 생성되지만 Factory Method 내에서 호출됩니다. Factory Method에 의해 반환된 객체는 종종 Product라고 합니다.

![alt](./images/Factory%20Method3.png)

_<서브클래스는 Factory Method에 의해 반환되는 객체의 클래스를 변경할 수 있습니다.>_

언뜻 보기에는 이 변경이 무의미해 보일 수 있습니다. 방금 생성자 호출을 프로그램의 한 부분에서 다른 부분으로 옮겼습니다. 그러나 이것을 고려하십시오. 이제 하위 클래스에서 Factory Method를 재정의하고 메소드에 의해 생성되는 Product 클래스를 변경할 수 있습니다.

하지만 약간의 제한이 있습니다. 하위 클래스는 이러한 제품에 공통 기본 클래스 또는 인터페이스가 있는 경우에만 다른 유형의 제품을 반환할 수 있습니다. 또한 기본 클래스의 Factory Method는 이 인터페이스로 선언된 리턴 유형을 가져야 합니다.

![alt](./images/Factory%20Method4.png)

_<모든 제품은 동일한 인터페이스를 따라야 합니다.>_

예를 들어, Truck 및 Ship 클래스는 모두 deliver라는 메서드를 선언하는 Transport 인터페이스를 구현해야 합니다. 각 클래스는 이 방법을 다르게 구현합니다. 트럭은 육로로 화물을 배달하고 선박은 해상으로 화물을 배달합니다. RoadLogistics 클래스의 Factory Method는 트럭 개체를 반환하는 반면 SeaLogistics 클래스의 Factory Method는 배를 반환합니다.

![alt](./images/Factory%20Method5.png)

_<모든 제품 클래스가 공통 인터페이스를 구현하는 한 해당 개체를 손상시키지 않고 클라이언트 코드에 전달할 수 있습니다.>_

Factory Method를 사용하는 코드(종종 클라이언트 코드라고 함)는 다양한 하위 클래스에서 반환된 실제 제품 간의 차이를 보지 못합니다. 클라이언트는 모든 제품을 추상 Transport로 취급합니다. 클라이언트는 모든 전송 개체에 전달 메서드가 있어야 한다는 것을 알고 있지만 정확히 어떻게 작동하는지는 클라이언트에게 중요하지 않습니다.

## 구조

![alt](./images/Factory%20Method6.png)

1. Product: 작성자와 해당 하위 클래스가 생성할 수 있는 모든 개체에 공통적인 인터페이스를 선언합니다.
2. Concrete Product: 제품 인터페이스의 다른 구현입니다.
3. Creator: 새 Product 개체를 반환하는 Factory Method를 선언합니다. 이 메서드의 반환 유형이 Product 인터페이스와 일치하는 것이 중요합니다. Factory Method를 추상으로 선언하여 모든 하위 클래스가 자체 버전의 메서드를 구현하도록 할 수 있습니다. 대안으로, 기본 Factory Method는 일부 기본 Product 유형을 리턴할 수 있습니다. 이름에도 불구하고 Product 제작은 제작자의 주요 책임이 아닙니다. 일반적으로 Creator 클래스에는 Product와 관련된 핵심 비즈니스 로직이 이미 있습니다. Factory Method는 이 로직을 구체적인 Product 클래스에서 분리하는 데 도움이 됩니다. 다음은 유추입니다. 대규모 소프트웨어 개발 회사에는 프로그래머를 위한 교육 부서가 있을 수 있습니다. 그러나 회사 전체의 주요 기능은 프로그래머를 생산하는 것이 아니라 여전히 코드를 작성하는 것입니다.
4. Concrete Creator: 기본 Factory Method를 재정의하므로 다른 유형의 제품을 반환합니다. Factory Method는 항상 새 인스턴스를 생성할 필요가 없습니다. 또한 캐시, 개체 풀 또는 다른 소스에서 기존 개체를 반환할 수도 있습니다.

## 의사 코드

이 예제는 클라이언트 코드를 구체적인 UI 클래스에 연결하지 않고 크로스 플랫폼 UI 요소를 만드는 데 Factory 메서드를 사용할 수 있는 방법을 보여줍니다.

![alt](./images/Factory%20Method7.png)

_<플랫폼 간 dialog 예시>_

기본 Dialog 클래스는 다른 UI 요소를 사용하여 창을 렌더링합니다. 다양한 운영 체제에서 이러한 요소는 약간 다르게 보일 수 있지만 여전히 일관되게 작동해야 합니다. Windows의 버튼은 여전히 ​​Linux의 버튼입니다.

Factory Method가 실행되면 각 운영 체제에 대해 Dialog 클래스의 논리를 다시 작성할 필요가 없습니다. 기본 Dialog 클래스 내에서 버튼을 생성하는 Factory Method를 선언하면 나중에 Factory Method에서 Windows 스타일 버튼을 반환하는 하위 클래스를 만들 수 있습니다. 그러면 하위 클래스는 기본 클래스에서 대부분의 코드를 상속하지만 Factory Method 덕분에 화면에 Windows 모양의 버튼을 렌더링할 수 있습니다.

이 패턴이 작동하려면 기본 Dialog 클래스가 추상 버튼과 함께 작동해야 합니다. 기본 클래스 또는 모든 구체적인 버튼이 뒤따르는 인터페이스입니다. 이런 식으로 Dialog 내의 코드는 작동하는 버튼 유형에 관계없이 기능을 유지합니다.

물론 이 접근 방식을 다른 UI 요소에도 적용할 수 있습니다. 그러나 대화 상자에 추가하는 각각의 새로운 Factory Method로 추상 팩토리 패턴에 더 가까워집니다. 두려워하지 마세요. 이 패턴에 대해서는 나중에 이야기하겠습니다.

```java
// Creator 클래스는 Product 클래스의 개체를 반환해야 하는 Factory Method를 선언합니다. Creator의 하위 클래스는 일반적으로 이 메서드의 구현을 제공합니다.
class Dialog is
    // Creator는 Factory Method의 일부 기본 구현을 제공할 수도 있습니다.
    abstract method createButton():Button

    // 이름에도 불구하고 Creator의 주요 책임은 제품을 만드는 것이 아닙니다. 일반적으로 Factory Method에서 반환된 Product 개체에 의존하는 몇 가지 핵심 비즈니스 로직을 포함합니다. 하위 클래스는 Factory Method를 재정의하고 다른 유형의 제품을 반환하여 비즈니스 로직을 간접적으로 변경할 수 있습니다.
    method render() is
        // Factory Method를 호출하여 Product 개체를 만듭니다.
        Button okButton = createButton()
        // 이제 Product를 사용하십시오.
        okButton.onClick(closeDialog)
        okButton.render()


// Concrete Creator는 Factory Method를 재정의하여 결과 제품의 유형을 변경합니다.
class WindowsDialog extends Dialog is
    method createButton():Button is
        return new WindowsButton()

class WebDialog extends Dialog is
    method createButton():Button is
        return new HTMLButton()


// Product 인터페이스는 모든 Concrete Product가 구현해야 하는 작업을 선언합니다.
interface Button is
    method render()
    method onClick(f)

// Concrete Product는 Product 인터페이스의 다양한 구현을 제공합니다.
class WindowsButton implements Button is
    method render(a, b) is
        // 버튼을 Windows 스타일로 렌더링합니다.
    method onClick(f) is
        // 기본 OS 클릭 이벤트를 바인딩합니다.

class HTMLButton implements Button is
    method render(a, b) is
        // 버튼의 HTML 표현을 반환합니다.
    method onClick(f) is
        // 웹 브라우저 클릭 이벤트를 바인딩합니다.

class Application is
    field dialog: Dialog

    // 애플리케이션은 현재 구성 또는 환경 설정에 따라 Creator의 유형을 선택합니다.
    method initialize() is
        config = readApplicationConfigFile()

        if (config.OS == "Windows") then
            dialog = new WindowsDialog()
        else if (config.OS == "Web") then
            dialog = new WebDialog()
        else
            throw new Exception("Error! Unknown operating system.")

    // 클라이언트 코드는 기본 인터페이스를 통해서라도 구체적인 Creator의 인스턴스와 함께 작동합니다. 클라이언트가 기본 인터페이스를 통해 Creator와 계속 작업하는 한 모든 Creator의 하위 클래스를 클라이언트에 전달할 수 있습니다.
    method main() is
        this.initialize()
        dialog.render()
```

## 적용 가능성

**코드에서 작업해야 하는 객체의 정확한 유형과 종속성을 미리 모르는 경우 Factory Method를 사용합니다.**

Factory Method는 Product 구성 코드와 실제로 Product를 사용하는 코드를 구분합니다. 따라서 코드의 나머지 부분과 독립적으로 Product 구성 코드를 확장하는 것이 더 쉽습니다.

예를 들어 앱에 새 Product 유형을 추가하려면 새 생성자 하위 클래스를 만들고 그 안에 있는 Factory Method를 재정의하기만 하면 됩니다.

**라이브러리나 프레임워크의 사용자에게 내부 구성 요소를 확장하는 방법을 제공하려는 경우 Factory Method를 사용합니다.**

상속은 아마도 라이브러리나 프레임워크의 기본 동작을 확장하는 가장 쉬운 방법일 것입니다. 그러나 프레임워크는 표준 구성 요소 대신 하위 클래스를 사용해야 한다는 것을 어떻게 인식할까요?

솔루션은 프레임워크 전체에서 구성 요소를 구성하는 코드를 단일 Factory Method로 줄이고 구성 요소 자체를 확장하는 것 외에도 누구나 이 메서드를 재정의할 수 있도록 하는 것입니다.

그것이 어떻게 작동하는지 봅시다. 오픈 소스 UI 프레임워크를 사용하여 앱을 작성한다고 상상해 보십시오. 앱에는 둥근 버튼이 있어야 하지만 프레임워크는 사각형 버튼만 제공합니다. 영광스러운 RoundButton 하위 클래스로 표준 Button 클래스를 확장합니다. 그러나 이제 기본 UIFramework 클래스에 기본 하위 클래스 대신 새 버튼 하위 클래스를 사용하도록 지시해야 합니다.

이를 달성하려면 기본 프레임워크 클래스에서 하위 클래스 UIWithRoundButtons를 만들고 해당 createButton 메서드를 재정의합니다. 이 메서드가 기본 클래스의 Button 개체를 반환하는 동안 하위 클래스가 RoundButton 개체를 반환하도록 합니다. 이제 UIFramework 대신 UIWithRoundButtons 클래스를 사용하십시오. 그리고 그것이 그것에 관한 것입니다.

**매번 재구축하는 대신 기존 개체를 재사용하여 시스템 리소스를 절약하려는 경우 Factory 메서드를 사용합니다.**

데이터베이스 연결, 파일 시스템 및 네트워크 리소스와 같이 리소스를 많이 사용하는 대규모 개체를 처리할 때 이러한 요구 사항이 자주 발생합니다.

기존 개체를 재사용하기 위해 수행해야 하는 작업에 대해 생각해 보겠습니다.

1. 먼저 생성된 모든 개체를 추적하기 위해 일부 저장소를 생성해야 합니다.
2. 누군가가 개체를 요청하면 프로그램은 해당 풀 내에서 사용 가능한 개체를 찾아야 합니다.
3. ... 그런 다음 클라이언트 코드로 반환합니다.
4. 사용 가능한 개체가 없으면 프로그램에서 새 개체를 만들고 풀에 추가해야 합니다.

그것은 많은 코드입니다. 그리고 중복 코드로 프로그램을 오염시키지 않도록 모두 한 곳에 넣어야 합니다.

아마도 이 코드를 배치할 수 있는 가장 분명하고 편리한 위치는 재사용하려는 객체의 클래스 생성자일 것입니다. 그러나 생성자는 항상 정의에 따라 새 개체를 반환해야 합니다. 기존 인스턴스를 반환할 수 없습니다.

따라서 새로운 객체를 생성하고 기존 객체를 재사용할 수 있는 일반 메서드가 필요합니다. 그것은 Factory 방식과 매우 흡사합니다.

## 구현방법

1. 모든 Product가 동일한 인터페이스를 따르도록 합니다. 이 인터페이스는 모든 Product에서 의미가 있는 메소드를 선언해야 합니다.
2. 생성자 클래스 내부에 빈 Factory Method를 추가합니다. 메소드의 리턴 유형은 공통 Product 인터페이스와 일치해야 합니다.
3. Creator의 코드에서 Product 생성자에 대한 모든 참조를 찾으십시오. Creator 생성 코드를 Factory Method로 추출하면서 하나씩 Factory Method에 대한 호출로 교체하십시오. 반품된 Product의 유형을 제어하기 위해 Factory Method에 임시 매개변수를 추가해야 할 수도 있습니다. 이 시점에서 Factory Method의 코드는 꽤 보기 흉할 수 있습니다. 인스턴스화할 Product 클래스를 선택하는 큰 스위치 문이 있을 수 있습니다. 하지만 걱정하지 마세요. 곧 해결해 드리겠습니다.
4. 이제 Factory Method에 나열된 각 Product 유형에 대한 Creator 서브클래스 세트를 작성하십시오. 하위 클래스에서 Factory Method를 재정의하고 기본 메서드에서 적절한 구성 코드 비트를 추출합니다.
5. 제품 유형이 너무 많고 모든 제품에 대한 하위 클래스를 만드는 것이 합리적이지 않은 경우 하위 클래스의 기본 클래스에서 제어 매개변수를 재사용할 수 있습니다. 예를 들어 다음과 같은 클래스 계층이 있다고 상상해 보십시오. AirMail 및 GroundMail과 같은 두 개의 하위 클래스가 있는 기본 Mail 클래스; 운송 클래스는 비행기, 트럭 및 기차입니다. AirMail 클래스는 Plane 객체만 사용하지만 GroundMail은 Truck 및 Train 객체 모두에서 작동할 수 있습니다. 두 경우를 모두 처리하기 위해 새 하위 클래스(예: TrainMail)를 만들 수 있지만 다른 옵션이 있습니다. 클라이언트 코드는 수신하려는 제품을 제어하기 위해 GroundMail 클래스의 Factory Method에 인수를 전달할 수 있습니다.
6. 모든 추출 후에 기본 Factory Method가 비어 있으면 추상화할 수 있습니다. 남아 있는 것이 있으면 메서드의 기본 동작으로 만들 수 있습니다.

## 장단점

### 장점

- Creator와 구체적인 Product 간의 긴밀한 결합을 피합니다.
- 단일 책임 원칙. 제품 생성 코드를 프로그램의 한 위치로 이동하여 코드를 더 쉽게 지원할 수 있습니다.
- 개방/폐쇄 원칙. 기존 클라이언트 코드를 손상시키지 않고 새로운 유형의 제품을 프로그램에 도입할 수 있습니다.

### 단점

- 패턴을 구현하기 위해 많은 새 하위 클래스를 도입해야 하므로 코드가 더 복잡해질 수 있습니다. 가장 좋은 시나리오는 생성자 클래스의 기존 계층 구조에 패턴을 도입할 때입니다.

### 자바스크립트 예제

```javascript
var Factory = function () {
  this.createEmployee = function (type) {
    var employee;

    if (type === "fulltime") {
      employee = new FullTime();
    } else if (type === "parttime") {
      employee = new PartTime();
    } else if (type === "temporary") {
      employee = new Temporary();
    } else if (type === "contractor") {
      employee = new Contractor();
    }

    employee.type = type;

    employee.say = function () {
      console.log(this.type + ": rate " + this.hourly + "/hour");
    };

    return employee;
  };
};

var FullTime = function () {
  this.hourly = "$12";
};

var PartTime = function () {
  this.hourly = "$11";
};

var Temporary = function () {
  this.hourly = "$10";
};

var Contractor = function () {
  this.hourly = "$15";
};

function run() {
  var employees = [];
  var factory = new Factory();

  employees.push(factory.createEmployee("fulltime"));
  employees.push(factory.createEmployee("parttime"));
  employees.push(factory.createEmployee("temporary"));
  employees.push(factory.createEmployee("contractor"));

  for (var i = 0, len = employees.length; i < len; i++) {
    employees[i].say();
  }
}
```
