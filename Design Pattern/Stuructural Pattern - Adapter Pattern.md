## 참고자료

https://refactoring.guru/design-patterns/adapter 를 번역하며 공부한 것을 정리한 내용입니다.

## 의도

어댑터 패턴은 호환되지 않는 인터페이스를 가진 객체들을 혼합할 수 있는 패턴입니다.

![title](./images/Stuructural%20Pattern%20-%20Adapter%20Pattern1.png){: width="500"}

## 문제

주식 시장 모니터링 앱을 만든다고 가정해봅시다. 이 앱은 XML 형식 기반으로 사용자에게 차트와 다이어그램을 제공합니다.

어느 시점에서 써드파티 분석 라이브러리를 사용하여 앱을 개선하기로 합니다. 이 때 라이브러르는 JSON 형식만 지원한다고 하면 문제가 발생합니다.

![title](./images/Stuructural%20Pattern%20-%20Adapter%20Pattern2.png){: width="500"}

XML을 지원하도록 라이브러리를 변경할 수 있습니다. 하지만 이 해결책은 라이브러리에 의존하는 기존 코드와 호환이 되지 않을 수 있습니다. 게다가 라이브러리의 소스코드에 접근할 수 없다면 이 해결책은 불가능한 방법이 됩니다.

## 해결

이 때 어댑터를 사용할 수 있으며, 이것은 한 객체의 인터페이스를 다른 객체가 이해할 수 있도록 변환하는 특수 객체입니다.

어댑터는 뒤에서 일어나는 변환의 복잡성을 숨기기 위해 객체중 하나를 래핑합니다. 래핑된 객체는 어댑터를 인식하지 못합니다.

예를 들어, 미터나 킬로미터로 동작하는 데이터를 피트나 마일로 동작하는 어댑터를 생각해볼 수 있습니다.

어댑터는 데이터를 다양한 형식으로 변경할 수 있을 뿐만 아니라, 다양한 인터페이스를 가진 객체가 협업할 수 있도록 도와줍니다.

작동 방식은 다음과 같습니다.

1. 어댑터는 기존 객체 중 하나와 호환되는 인터페이스를 가져옵니다.
2. 이 인터페이스를 사용하면 기존 객체가 어댑터의 메서드를 안전하게 호출할 수 있습니다.
3. 호출을 수신하면 어댑터는 요청을 두번째 객체에 전달하고, 두번째 객체가 예상하는 형식과 순서로 전달합니다.

![title](./images/Stuructural%20Pattern%20-%20Adapter%20Pattern3.png){: width="500"}

주식 시장 앱으로 돌아가서 이제 XML-JSON 어댑터를 만들고, 이 어댑터를 통해서만 라이브러리와 통신하도록 변경합니다. 어댑터가 호출을 수신하면 들어오는 XML 형식을 JSON 형식으로 변경하고, 라이브러리에 전달합니다.

## 현실 유사성

![title](./images/Stuructural%20Pattern%20-%20Adapter%20Pattern4.png){: width="500"}

전원 플래그 어댑터를 예로 들 수 있습니다. 전원 플러그 표준은 국가마다 다르지만, 전원 플래그 어댑터를 사용하여 문제를 해결할 수 있습니다.

## 구조

### Object adapter

이 방식은 객체 구성 원칙을 사용합니다. 모든 프로그래밍 언어로 구현할 수 있습니다.

![title](./images/Stuructural%20Pattern%20-%20Adapter%20Pattern5.png){: width="500"}

1. 클라이언트는 기존 비지니스 로직을 포함하는 클래스입니다.
2. 클라이언트 인터페이스는 다른 클래스가 클라이언트 코드와 협력할 때 따라야 하는 프로토콜을 구독하니다.
3. 서비스는 일반적으로 써드파티나 레거시와 같은 클래스입니다. 클라이언트는 이 클래스와 호환되지 않는 인터페이스를 가지고 있기 때문에 직접적으로 통신할 수 없습니다.
4. 어댑터는 클라이언트와 서비스에서 모두 작동할 수 있는 클래스이며, 서비스 객체를 래핑하는 동안 클라이언트 인터페이스를 구현합니다. 어댑터는 어댑터 인터페이스를 통해 클라이언트로부터 호출을 수신하고 래핑된 서비스 객체에 대한 호출로 변환합니다.
5. 클라이언트 코드는 어댑터 클래스에 직접적으로 연결되지 않으므로 기존 클라이언트 코드를 손상시키지 않고 새로운 유형의 어댑터를 도입할 수 있습니다. 이것은 서비스 클래스의 인터페이스가 변경되거나 대체될 때 유용하게 사용할 수 있습니다.

### Class adapter

이 구현은 상속을 사용합니다. C++와 같이 다중 상속을 지원하는 프로그래밍 언어에서만 사용할 수 있습니다.

![title](./images/Stuructural%20Pattern%20-%20Adapter%20Pattern6.png){: width="500"}

1. 클래스 어댑터는 클라이언트와 서비스 모두에서 동작을 상속 받으므로, 객체를 래핑할 필요가 없습니다. 오버라이드 된 메서드에서 변환이 일어나며, 클라이언트는 클래스 어댑터와 통신할 수 있습니다.

## 가짜 코드

사각못과 둥근 구멍 사이의 충돌을 기반으로 한 가짜 코드입니다.

```java
// 호환되는 두개의 인터페이스가 있다고 가정합니다. (둥근 구멍과 둥근못)
class RoundHole is
    constructor RoundHole(radius) { ... }

    method getRadius() is
        // Return the radius of the hole.

    method fits(peg: RoundPeg) is
        return this.getRadius() >= peg.getRadius()

class RoundPeg is
    constructor RoundPeg(radius) { ... }

    method getRadius() is
        // Return the radius of the peg.


// 그러나 호환되지 않는 사각못이 있습니다.
class SquarePeg is
    constructor SquarePeg(width) { ... }

    method getWidth() is
        // Return the square peg width.


// 어댑터 클래스를 사용하면 사각못을 둥근 구멍에 맞출 수 있습니다.
// 어댑터 객체가 동작하도록 둥근못 클래스를 확장합니다.
class SquarePegAdapter extends RoundPeg is
    // 어댑터에는 사각못 클래스의 인스턴스가 포함되어 있습니다.
    private field peg: SquarePeg

    constructor SquarePegAdapter(peg: SquarePeg) is
        this.peg = peg

    method getRadius() is
        // 어댑터는 getRadius 메서드를 사진 둥근못 클래스인것처럼 가장합니다.
        return peg.getWidth() * Math.sqrt(2) / 2


// 클라이언트 코드
hole = new RoundHole(5)
rpeg = new RoundPeg(5)
hole.fits(rpeg) // true

small_sqpeg = new SquarePeg(5)
large_sqpeg = new SquarePeg(10)
hole.fits(small_sqpeg) // this won't compile (incompatible types)

small_sqpeg_adapter = new SquarePegAdapter(small_sqpeg)
large_sqpeg_adapter = new SquarePegAdapter(large_sqpeg)
hole.fits(small_sqpeg_adapter) // true
hole.fits(large_sqpeg_adapter) // false
```

## 적용 가능성

**기존 클래스를 사용하고 싶지만, 인터페이스가 서비스 클래스와 호환되지 않을 때 사용합니다.**

어댑터 패턴을 사용하면 기존 코드와 레거시 클래스, 써드파티 클래스, 그 외 이상한 인터페이스의 서비스 클래스 간의 중간 역할을 하는 클래스를 만들 수 있습니다.

**상위 클래스에 추가할 수 없는 공통 기능을 기존 하위 클래스에서 재사용하고 싶을때 사용합니다.**

각 하위 클래스를 확장하고 누락된 기능을 새 하위 클래스에 넣을 수 있습니다. 그러나 모든 새 하위 클래스에 코드를 복제해야 하며, 이는 나쁜 냄새가 나는 행위입니다.

더 좋은 방법은 누락된 기능을 어댑터 클래스에 넣는 것입니다. 그 다음 어댑터 내부의 누락된 기능이 있는 객체를 래핑하여 필요한 기능을 동적으로 얻을 수 있습니다.

## 구현 방법

1. 호환되지 않는 인터페이스를 사용하는 클래스가 두 개 이상인지 확인합니다.
   - 변경할 수 없는 서비스 클래스 (보통 써브파티 혹은 종속성이 많은 레거시 클래스)
   - 서비스 클래스를 사용하는 클라이언트 클래스
2. 클라이언트 인터페이스를 선언하고 서비스 클래스와 통신을 하도록 작성합니다.
3. 어댑터 클래스를 만들고 클라이언트 인터페이스를 따르도록 합니다. 모든 메서드는 일단 비워둡니다.
4. 서비스 객체에 대한 참조를 저장할 필드를 어댑터 클래스에 추가합니다.
5. 어댑터 클래스에서 클라이언트 인터페이스에 해당하는 메서드를 구현합니다. 어댑터는 인터페이스 혹은 데이터 형식만 변경하고, 실제 작업은 서비스 객체에 위임합니다.
6. 클라이언트는 클라이언트 인터페이스를 통해 어댑터를 사용합니다.

## 장단점

### 장점

- 단일 책임 원칙 - 비지니스 로직에서 인터페이스 또는 데이터 변환 코드를 분리할 수 있습니다.
- 개방/페쇄 원칙 - 기존 클라이언트 코드를 손상시키지 않고 새로운 유형의 어댑터를 도입할 수 있습니다.

### 단점

- 새로운 인터페이스와 클래스 세트를 도입해야하기 때문에 코드의 복잡성이 증가할 수 있습니다. 경우에 따라 서비스 클래스의 코드를 변경하는 것이 더 간단한 방법일 수 있습니다.
