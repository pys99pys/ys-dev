# Abstract Factory

https://refactoring.guru/design-patterns/abstract-factory 를 공부하며 정리한 내용입니다.

## Abstract Factory란?

Abstract Factory는 구체적인 클래스를 지정하지 않고 관련 개체의 패밀리를 생성할 수 있는 생성 디자인 패턴입니다.

![alt](./images/Abstract%20Factory1.png)

## 문제

가구 매장 시뮬레이터를 만들고 있다고 상상해보십시오. 코드는 다음을 나타내는 클래스로 구성됩니다.

1. 관련 제품 제품군, 예: 의자 + 소파 + 커피 테이블.
2. 이 제품군의 여러 변형. 예를 들어, 의자 + 소파 + 커피 테이블. 제품은 Modern, Victorian, ArtDeco 변형으로 제공됩니다.

![alt](./images/Abstract%20Factory2.png)

_<제품군 및 해당 변형.>_

동일한 패밀리의 다른 객체와 일치하도록 개별 가구 객체를 작성하는 방법이 필요합니다. 고객은 어울리지 않는 가구를 받으면 매우 화를 냅니다.

![alt](./images/Abstract%20Factory3.png)

_<모던 스타일의 소파는 빅토리아 스타일의 의자와 어울리지 않습니다.>_

또한 프로그램에 새로운 제품이나 제품군을 추가할 때 기존 코드를 변경하고 싶지 않습니다. 가구 공급업체는 카탈로그를 매우 자주 업데이트하므로 발생할 때마다 핵심 코드를 변경하고 싶지 않을 것입니다.

## 해결책

Abstract Factory 패턴이 제안하는 첫 번째 사항은 제품군의 개별 제품(예: 의자, 소파 또는 커피 테이블)에 대한 인터페이스를 명시적으로 선언하는 것입니다. 그런 다음 제품의 모든 변형이 이러한 인터페이스를 따르도록 할 수 있습니다. 예를 들어, 모든 의자 변형은 Chair 인터페이스를 구현할 수 있습니다. 모든 커피 테이블 변형은 CoffeeTable 인터페이스 등을 구현할 수 있습니다.

![alt](./images/Abstract%20Factory4.png)

_<동일한 개체의 모든 변형은 단일 클래스 계층으로 이동해야 합니다.>_

다음 단계는 제품군의 일부인 모든 제품(예: createChair, createSofa 및 createCoffeeTable)에 대한 생성 방법 목록이 있는 인터페이스인 Abstract Factory를 선언하는 것입니다. 이러한 메서드는 이전에 추출한 인터페이스인 Chair, Sofa, CoffeeTable 등으로 표현되는 추상 제품 유형을 반환해야 합니다.

![alt](./images/Abstract%20Factory5.png)

_<각 구현 팩토리는 특정 제품 변형에 해당합니다.>_

이제 제품 변형은 어떻습니까? 제품군의 각 변형에 대해 AbstractFactory 인터페이스를 기반으로 하는 별도의 팩토리 클래스를 생성합니다. 팩토리는 특정 종류의 제품을 반환하는 클래스입니다. 예를 들어 ModernFurnitureFactory는 ModernChair, ModernSofa 및 ModernCoffeeTable 개체만 생성할 수 있습니다.

클라이언트 코드는 각각의 추상 인터페이스를 통해 팩토리와 제품 모두에서 작동해야 합니다. 이를 통해 실제 클라이언트 코드를 손상시키지 않고 클라이언트 코드에 전달하는 팩토리 유형과 클라이언트 코드가 수신하는 제품 변형을 변경할 수 있습니다.

![alt](./images/Abstract%20Factory6.png)

_<클라이언트는 작업하는 팩토리의 구체적인 클래스에 대해 신경 쓰지 않아야 합니다.>_

클라이언트가 공장에서 의자를 생산하기를 원한다고 가정해 보겠습니다. 클라이언트는 공장의 클래스를 알 필요가 없으며 어떤 종류의 의자를 가져오는지 중요하지 않습니다. 모던 모델이든 빅토리아 스타일의 의자이든 클라이언트는 추상적인 Chair 인터페이스를 사용하여 모든 의자를 동일한 방식으로 다루어야 합니다. 이 접근 방식에서 클라이언트가 의자에 대해 아는 유일한 것은 그것이 어떤 방식으로든 sitOn 메서드를 구현한다는 것입니다. 또한 어떤 변형의 의자가 반환되든 동일한 공장 개체에서 생산된 소파 또는 커피 테이블의 유형과 항상 일치합니다.

명확히 해야 할 것이 한 가지 더 남아 있습니다. 클라이언트가 추상 인터페이스에만 노출되는 경우 실제 팩토리 객체를 생성하는 것은 무엇입니까? 일반적으로 애플리케이션은 초기화 단계에서 구체적인 팩토리 객체를 생성합니다. 그 직전에 앱은 구성 또는 환경 설정에 따라 공장 유형을 선택해야 합니다.

## 구조

![alt](./images/Abstract%20Factory7.png)

1. Abstract Product: 제품군을 구성하는 별개의 관련 제품 세트에 대한 인터페이스를 선언합니다.
2. Concrete Product: 변형별로 그룹화된 추상 제품의 다양한 구현입니다. 각 추상 제품(의자/소파)은 주어진 모든 변형(Victorian/Modern)으로 구현되어야 합니다.
3. Abstract Factory: 는 각각의 추상 제품을 생성하기 위한 메소드 세트를 선언합니다.
4. Concrete Factory: Abstract Factory의 생성 방법을 구현합니다. 각 콘크리트 공장은 제품의 특정 변형에 해당하며 해당 제품 변형만 생성합니다.
5. Concrete Factory는 구체적인 제품을 인스턴스화하지만 생성 방법의 서명은 해당 Abstract Product를 반환해야 합니다. 이렇게 하면 팩토리를 사용하는 클라이언트 코드가 팩토리에서 가져온 제품의 특정 변형에 연결되지 않습니다. 클라이언트는 추상 인터페이스를 통해 개체와 통신하는 한 모든 구체적인 공장/제품 변형으로 작업할 수 있습니다.

## 의사 코드

이 예제는 생성된 모든 요소를 ​​선택한 운영 체제와 일관되게 유지하면서 클라이언트 코드를 구체적인 UI 클래스에 연결하지 않고 플랫폼 간 UI 요소를 생성하는 데 Abstract Factory 패턴을 사용하는 방법을 보여줍니다.

![alt](./images/Abstract%20Factory8.png)

_<플랫폼 간 UI 클래스 예시.>_

크로스 플랫폼 애플리케이션의 동일한 UI 요소는 유사하게 동작할 것으로 예상되지만 다른 운영 체제에서는 약간 다르게 보입니다. 또한 UI 요소가 현재 운영 체제의 스타일과 일치하는지 확인하는 것이 귀하의 일입니다. 프로그램이 Windows에서 실행될 때 macOS 컨트롤을 렌더링하는 것을 원하지 않을 것입니다.

Abstract Factory 인터페이스는 클라이언트 코드가 다양한 유형의 UI 요소를 생성하는 데 사용할 수 있는 일련의 생성 방법을 선언합니다. 구체적인 팩토리는 특정 운영 체제에 해당하고 해당 특정 OS와 일치하는 UI 요소를 생성합니다.

작동 방식은 다음과 같습니다. 애플리케이션이 시작될 때 현재 운영 체제 유형을 확인합니다. 앱은 이 정보를 사용하여 운영 체제와 일치하는 클래스에서 팩토리 객체를 생성합니다. 나머지 코드는 이 팩토리를 사용하여 UI 요소를 만듭니다. 이렇게 하면 잘못된 요소가 생성되는 것을 방지할 수 있습니다.

이 접근 방식을 사용하면 클라이언트 코드가 추상 인터페이스를 통해 이러한 객체와 함께 작동하는 한 팩토리 및 UI 요소의 구체적인 클래스에 의존하지 않습니다. 이렇게 하면 클라이언트 코드가 나중에 추가할 수 있는 다른 팩토리 또는 UI 요소를 지원할 수도 있습니다.

결과적으로 새로운 변형의 UI 요소를 앱에 추가할 때마다 클라이언트 코드를 수정할 필요가 없습니다. 이러한 요소를 생성하는 새 팩토리 클래스를 만들고 앱의 초기화 코드를 약간 수정하여 적절할 때 해당 클래스를 선택하기만 하면 됩니다.

```java
// Abstract Factory 인터페이스는 다른 추상 제품을 반환하는 메서드 집합을 선언합니다. 이러한 제품을 패밀리라고 하며 상위 수준의 테마 또는 개념으로 연결됩니다. 한 가족의 제품은 일반적으로 서로 협력할 수 있습니다. 제품군에는 여러 변형이 있을 수 있지만 한 변형의 제품은 다른 변형의 제품과 호환되지 않습니다.
interface GUIFactory is
    method createButton():Button
    method createCheckbox():Checkbox


// Concreate Factory는 단일 변형에 속하는 제품군을 생산합니다. 공장은 결과 제품이 호환 가능함을 보장합니다. 구체적인 팩토리 메소드의 서명은 추상 제품을 반환하는 반면 메소드 내부에서는 구체적인 제품이 인스턴스화됩니다.
class WinFactory implements GUIFactory is
    method createButton():Button is
        return new WinButton()
    method createCheckbox():Checkbox is
        return new WinCheckbox()

// 각 Concreate Factory에는 해당 제품 변형이 있습니다.
class MacFactory implements GUIFactory is
    method createButton():Button is
        return new MacButton()
    method createCheckbox():Checkbox is
        return new MacCheckbox()


// 제품군의 각 개별 제품에는 기본 인터페이스가 있어야 합니다. 제품의 모든 변형은 이 인터페이스를 구현해야 합니다.
interface Button is
    method paint()

// Concreate Product는 해당 Concrete Factory에서 생성됩니다.
class WinButton implements Button is
    method paint() is
        // 버튼을 Windows 스타일로 렌더링합니다.

class MacButton implements Button is
    method paint() is
        // 버튼을 macOS 스타일로 렌더링합니다.

// 다음은 다른 제품의 기본 인터페이스입니다. 모든 제품은 서로 상호 작용할 수 있지만 적절한 상호 작용은 동일한 구체적인 변형의 제품 간에만 가능합니다.
interface Checkbox is
    method paint()

class WinCheckbox implements Checkbox is
    method paint() is
        // 체크박스를 Windows 스타일로 렌더링합니다.

class MacCheckbox implements Checkbox is
    method paint() is
        // 체크박스를 macOS 스타일로 렌더링합니다.

// 클라이언트 코드는 GUIFactory, Button 및 Checkbox와 같은 추상 유형을 통해서만 팩토리 및 제품과 함께 작동합니다. 이를 통해 팩토리 또는 제품 하위 클래스를 손상시키지 않고 클라이언트 코드에 전달할 수 있습니다.
class Application is
    private field factory: GUIFactory
    private field button: Button

    constructor Application(factory: GUIFactory) is
        this.factory = factory

    method createUI() is
        this.button = factory.createButton()

    method paint() is
        button.paint()


// 응용 프로그램은 현재 구성 또는 환경 설정에 따라 공장 유형을 선택하고 런타임(일반적으로 초기화 단계)에 생성합니다.
class ApplicationConfigurator is
    method main() is
        config = readApplicationConfigFile()

        if (config.OS == "Windows") then
            factory = new WinFactory()
        else if (config.OS == "Mac") then
            factory = new MacFactory()
        else
            throw new Exception("Error! Unknown operating system.")

        Application app = new Application(factory)
```

## 적용 가능성

**코드가 관련 제품의 다양한 제품군과 함께 작동해야 하지만 해당 제품의 구체적인 클래스에 의존하고 싶지 않은 경우 Abstract Factory를 사용하십시오.**

Abstract Factory는 제품군의 각 클래스에서 객체를 생성하기 위한 인터페이스를 제공합니다. 코드가 이 인터페이스를 통해 객체를 생성하는 한 앱에서 이미 생성된 제품과 일치하지 않는 잘못된 제품 변형을 생성하는 것에 대해 걱정할 필요가 없습니다.

- 기본 책임을 흐리게 하는 팩토리 메소드 세트가 있는 클래스가 있는 경우 Abstract Factory 구현을 고려하십시오.
- 잘 설계된 프로그램에서 각 클래스는 한 가지만 담당합니다. 클래스가 여러 제품 유형을 처리할 때 팩토리 메소드를 독립형 팩토리 클래스 또는 완전한 Abstract Factory 구현으로 추출하는 것이 좋습니다.

## 구현방법

1. 이러한 제품의 변형에 대한 고유한 제품 유형의 매트릭스를 매핑합니다.
2. 모든 제품 유형에 대한 Abstract Product 인터페이스를 선언합니다. 그런 다음 모든 Concreate Product 클래스가 이러한 인터페이스를 구현하도록 합니다.
3. 모든 Abstract Product에 대한 생성 메서드 집합으로 Abstract Factory 인터페이스를 선언합니다.
4. 각 제품 변형에 대해 하나씩 Concreate Factory 클래스 세트를 구현하십시오.
5. 앱 어딘가에 팩토리 초기화 코드를 만듭니다. 애플리케이션 구성 또는 현재 환경에 따라 Concreate Factory 클래스 중 하나를 인스턴스화해야 합니다. 이 팩토리 객체를 제품을 구성하는 모든 클래스에 전달하십시오.
6. 코드를 스캔하고 제품 생성자에 대한 모든 직접 호출을 찾습니다. 팩토리 객체에 대한 적절한 생성 메서드에 대한 호출로 교체합니다.

## 장단점

### 장점

- 공장에서 받는 제품이 서로 호환되는지 확인할 수 있습니다.
- 구체적인 제품과 클라이언트 코드 간의 긴밀한 결합을 피합니다.
- 단일 책임 원칙. 제품 생성 코드를 한 곳으로 추출하여 코드를 더 쉽게 지원할 수 있습니다.
- 개방/폐쇄 원칙. 기존 클라이언트 코드를 손상시키지 않고 제품의 새로운 변형을 도입할 수 있습니다.

### 단점

- 많은 새로운 인터페이스와 클래스가 패턴과 함께 도입되기 때문에 코드가 생각보다 복잡해질 수 있습니다.

### 자바스크립트 예제

```javascript
function Employee(name) {
  this.name = name;

  this.say = function () {
    console.log("I am employee " + name);
  };
}

function EmployeeFactory() {
  this.create = function (name) {
    return new Employee(name);
  };
}

function Vendor(name) {
  this.name = name;

  this.say = function () {
    console.log("I am vendor " + name);
  };
}

function VendorFactory() {
  this.create = function (name) {
    return new Vendor(name);
  };
}

function run() {
  var persons = [];
  var employeeFactory = new EmployeeFactory();
  var vendorFactory = new VendorFactory();

  persons.push(employeeFactory.create("Joan DiSilva"));
  persons.push(employeeFactory.create("Tim O'Neill"));
  persons.push(vendorFactory.create("Gerald Watson"));
  persons.push(vendorFactory.create("Nicole McNight"));

  for (var i = 0, len = persons.length; i < len; i++) {
    persons[i].say();
  }
}
```
