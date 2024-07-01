# Proxy

https://refactoring.guru/design-patterns/proxy 를 공부하며 정리한 내용입니다.

## Proxy란?

Proxy는 다른 개체에 대한 대체 또는 자리 표시자를 제공할 수 있는 구조적 디자인 패턴입니다. Proxy는 원래 개체에 대한 액세스를 제어하므로 요청이 원래 개체에 전달되기 전이나 후에 수행할 수 있습니다.

![alt](./images/Proxy1.png)

## 문제

개체에 대한 액세스를 제어하려는 이유는 무엇입니까? 다음은 예입니다. 방대한 양의 시스템 리소스를 소비하는 방대한 개체가 있습니다. 때때로 필요하지만 항상 그런 것은 아닙니다.

![alt](./images/Proxy2.png)

_<데이터베이스 쿼리는 정말 느릴 수 있습니다.>_

지연 초기화를 구현할 수 있습니다. 실제로 필요할 때만 이 객체를 생성하세요. 객체의 모든 클라이언트는 지연된 초기화 코드를 실행해야 합니다. 불행히도, 이것은 아마도 많은 코드 중복을 야기할 것입니다.

이상적인 세계에서는 이 코드를 객체의 클래스에 직접 넣고 싶지만 항상 가능한 것은 아닙니다. 예를 들어 클래스가 폐쇄된 타사 라이브러리의 일부일 수 있습니다.

## 해결책

Proxy 패턴은 원래 서비스 객체와 동일한 인터페이스로 새 Proxy 클래스를 생성하도록 제안합니다. 그런 다음 Proxy 개체를 원래 개체의 모든 클라이언트에 전달하도록 앱을 업데이트합니다. 클라이언트로부터 요청을 받으면 Proxy는 실제 서비스 객체를 생성하고 모든 작업을 이 객체에 위임합니다.

![alt](./images/Proxy3.png)

_<Proxy는 데이터베이스 개체로 가장합니다. 클라이언트나 실제 데이터베이스 개체가 알지 못하는 상태에서 지연 초기화 및 결과 캐싱을 처리할 수 있습니다.>_

그러나 이점이 무엇입니까? 클래스의 기본 로직 이전이나 이후에 무언가를 실행해야 하는 경우 Proxy를 사용하면 해당 클래스를 변경하지 않고도 이를 수행할 수 있습니다. Proxy는 원래 클래스와 동일한 인터페이스를 구현하므로 실제 서비스 개체를 기대하는 모든 클라이언트에 전달할 수 있습니다.

## 현실 유사성

![alt](./images/Proxy4.png)

_<신용 카드는 현금과 마찬가지로 지불에 사용할 수 있습니다.>_

신용 카드는 은행 계좌의 대리인이며 현금 묶음의 대리인입니다. 둘 다 동일한 인터페이스를 구현합니다. 결제에 사용할 수 있습니다. 많은 현금을 가지고 다닐 필요가 없기 때문에 소비자는 기분이 좋습니다. 상점 주인은 또한 예금을 잃어버리거나 은행에 가는 길에 강도를 당할 위험 없이 거래 수입이 상점의 은행 계좌에 전자적으로 추가되기 때문에 만족합니다.

## 구조

![alt](./images/Proxy5.png)

1. Service Interface: 서비스의 인터페이스를 선언합니다. Proxy는 서비스 개체로 위장할 수 있도록 이 인터페이스를 따라야 합니다.
2. Service: 몇 가지 유용한 비즈니스 로직을 제공하는 클래스입니다.
3. Proxy 클래스: 서비스 개체를 가리키는 참조 필드가 있습니다. Proxy가 처리(예: 초기화 지연, 로깅, 액세스 제어, 캐싱 등)를 완료한 후 요청을 서비스 개체에 전달합니다. 일반적으로 Proxy는 서비스 개체의 전체 수명 주기를 관리합니다.
4. 클라이언트는 동일한 인터페이스를 통해 서비스와 Proxy 모두에서 작업해야 합니다. 이렇게 하면 서비스 개체가 필요한 모든 코드에 Proxy를 전달할 수 있습니다.

## 의사 코드

이 예는 Proxy 패턴이 제3자 YouTube 통합 라이브러리에 지연 초기화 및 캐싱을 도입하는 데 어떻게 도움이 되는지 보여줍니다.

![alt](./images/Proxy6.png)

_<Proxy를 사용하여 서비스 결과를 캐싱합니다.>_

라이브러리는 비디오 다운로드 수업을 제공합니다. 그러나 매우 비효율적입니다. 클라이언트 애플리케이션이 동일한 비디오를 여러 번 요청하는 경우 라이브러리는 처음 다운로드한 파일을 캐싱하고 재사용하는 대신 계속해서 비디오를 다운로드합니다.

Proxy 클래스는 원래 다운로더와 동일한 인터페이스를 구현하고 모든 작업을 위임합니다. 그러나 앱이 동일한 비디오를 여러 번 요청하면 다운로드한 파일을 추적하고 캐시된 결과를 반환합니다.

```java
// 원격 서비스의 인터페이스입니다.
interface ThirdPartyYouTubeLib is
    method listVideos()
    method getVideoInfo(id)
    method downloadVideo(id)

// 서비스 커넥터의 구체적인 구현. 이 클래스의 메서드는 YouTube에서 정보를 요청할 수 있습니다. 요청 속도는 사용자의 인터넷 연결과 YouTube 연결에 따라 다릅니다. 모든 요청이 동일한 정보를 요청하더라도 많은 요청이 동시에 실행되면 애플리케이션 속도가 느려집니다.
class ThirdPartyYouTubeClass implements ThirdPartyYouTubeLib is
    method listVideos() is
        // YouTube에 API 요청을 보냅니다.

    method getVideoInfo(id) is
        // 일부 비디오에 대한 메타데이터를 가져옵니다.

    method downloadVideo(id) is
        // YouTube에서 동영상 파일을 다운로드합니다.

// 대역폭을 절약하기 위해 요청 결과를 캐시하고 일정 기간 동안 보관할 수 있습니다. 그러나 이러한 코드를 서비스 클래스에 직접 넣는 것은 불가능할 수 있습니다. 예를 들어, 타사 라이브러리의 일부로 제공되거나 '최종'으로 정의될 수 있습니다. 그렇기 때문에 서비스 클래스와 동일한 인터페이스를 구현하는 새 Proxy 클래스에 캐싱 코드를 넣습니다. 실제 요청을 보내야 하는 경우에만 서비스 개체에 위임합니다.
class CachedYouTubeClass implements ThirdPartyYouTubeLib is
    private field service: ThirdPartyYouTubeLib
    private field listCache, videoCache
    field needReset

    constructor CachedYouTubeClass(service: ThirdPartyYouTubeLib) is
        this.service = service

    method listVideos() is
        if (listCache == null || needReset)
            listCache = service.listVideos()
        return listCache

    method getVideoInfo(id) is
        if (videoCache == null || needReset)
            videoCache = service.getVideoInfo(id)
        return videoCache

    method downloadVideo(id) is
        if (!downloadExists(id) || needReset)
            service.downloadVideo(id)

// 서비스 개체와 직접 작업하던 GUI 클래스는 인터페이스를 통해 서비스 개체와 함께 작동하는 한 변경되지 않습니다. 둘 다 동일한 인터페이스를 구현하므로 실제 서비스 개체 대신 Proxy 개체를 안전하게 전달할 수 있습니다.
class YouTubeManager is
    protected field service: ThirdPartyYouTubeLib

    constructor YouTubeManager(service: ThirdPartyYouTubeLib) is
        this.service = service

    method renderVideoPage(id) is
        info = service.getVideoInfo(id)
        // 비디오 페이지를 렌더링합니다.

    method renderListPanel() is
        list = service.listVideos()
        // 비디오 썸네일 목록을 렌더링합니다.

    method reactOnUserInput() is
        renderVideoPage()
        renderListPanel()

// 애플리케이션은 즉시 Proxy를 구성할 수 있습니다.
class Application is
    method init() is
        aYouTubeService = new ThirdPartyYouTubeClass()
        aYouTubeProxy = new CachedYouTubeClass(aYouTubeService)
        manager = new YouTubeManager(aYouTubeProxy)
        manager.reactOnUserInput()
```

## 적용 가능성

Proxy 패턴을 활용하는 방법은 수십 가지가 있습니다. 가장 많이 사용되는 용도를 살펴보겠습니다.

**지연 초기화(가상 Proxy). 이것은 때때로 필요하지만 항상 가동되어 시스템 리소스를 낭비하는 무거운 서비스 개체가 있는 경우입니다.**

앱이 시작될 때 객체를 생성하는 대신, 객체 초기화가 정말로 필요한 시점으로 지연될 수 있습니다.

**액세스 제어(보호 Proxy). 특정 클라이언트만 서비스 개체를 사용할 수 있도록 하려는 경우입니다. 예를 들어 개체가 운영 체제의 중요한 부분이고 클라이언트가 다양한 실행 응용 프로그램(악의적인 응용 프로그램 포함)인 경우입니다.**

Proxy는 클라이언트의 자격 증명이 일부 기준과 일치하는 경우에만 서비스 개체에 요청을 전달할 수 있습니다.

**원격 서비스의 로컬 실행(원격 Proxy). 서비스 개체가 원격 서버에 있는 경우입니다.**

이 경우 Proxy는 네트워크를 통해 클라이언트 요청을 전달하여 네트워크 작업의 모든 불쾌한 세부 사항을 처리합니다.

**로깅 요청(로깅 Proxy). 서비스 개체에 대한 요청 기록을 유지하려는 경우입니다.**

Proxy는 서비스에 전달하기 전에 각 요청을 기록할 수 있습니다.

**캐싱 요청 결과(캐싱 Proxy). 이것은 특히 결과가 상당히 큰 경우 클라이언트 요청의 결과를 캐시하고 이 캐시의 수명 주기를 관리해야 할 때입니다.**

Proxy는 항상 동일한 결과를 생성하는 반복 요청에 대해 캐싱을 구현할 수 있습니다. Proxy는 요청의 매개변수를 캐시 키로 사용할 수 있습니다.

**스마트 참조. 이것은 무거운 객체를 사용하는 클라이언트가 없을 때 해제할 수 있어야 할 때입니다.**

Proxy는 서비스 개체 또는 해당 결과에 대한 참조를 얻은 클라이언트를 추적할 수 있습니다. 때때로 Proxy는 클라이언트를 통해 클라이언트가 여전히 활성 상태인지 확인할 수 있습니다. 클라이언트 목록이 비어 있으면 Proxy가 서비스 개체를 닫고 기본 시스템 리소스를 해제할 수 있습니다.

Proxy는 클라이언트가 서비스 개체를 수정했는지 여부도 추적할 수 있습니다. 그런 다음 변경되지 않은 개체는 다른 클라이언트에서 재사용할 수 있습니다.

## 구현방법

1. 기존 서비스 인터페이스가 없는 경우 Proxy와 서비스 객체를 교환할 수 있도록 생성합니다. 서비스 클래스에서 인터페이스를 추출하는 것이 항상 가능한 것은 아닙니다. 해당 인터페이스를 사용하려면 서비스의 모든 클라이언트를 변경해야 하기 때문입니다. 플랜 B는 Proxy를 서비스 클래스의 하위 클래스로 만드는 것이며, 이러한 방식으로 서비스의 인터페이스를 상속합니다.
2. Proxy 클래스를 만듭니다. 서비스에 대한 참조를 저장하기 위한 필드가 있어야 합니다. 일반적으로 Proxy는 서비스의 전체 수명 주기를 만들고 관리합니다. 드문 경우지만 클라이언트가 생성자를 통해 서비스를 Proxy에 전달합니다.
3. 목적에 따라 Proxy 메소드를 구현하십시오. 대부분의 경우 일부 작업을 수행한 후 Proxy는 작업을 서비스 개체에 위임해야 합니다.
4. 클라이언트가 Proxy를 받을지 실제 서비스를 받을지 결정하는 생성 방법을 도입하는 것을 고려하십시오. 이것은 Proxy 클래스의 간단한 정적 메서드이거나 완전한 팩토리 메서드일 수 있습니다.
5. 서비스 개체에 대해 지연 초기화 구현을 고려하십시오.

## 장단점

### 장점

- 클라이언트가 알지 못하는 상태에서 서비스 개체를 제어할 수 있습니다.
- 클라이언트가 신경 쓰지 않을 때 서비스 개체의 수명 주기를 관리할 수 있습니다.
- 프록시는 서비스 개체가 준비되지 않았거나 사용할 수 없는 경우에도 작동합니다.
- 개방/폐쇄 원칙. 서비스나 클라이언트를 변경하지 않고 새 프록시를 도입할 수 있습니다.

### 단점

- 많은 새 클래스를 도입해야 하므로 코드가 더 복잡해질 수 있습니다.
- 서비스 응답이 늦어질 수 있습니다.

### 자바스크립트 예제

```javascript
function GeoCoder() {
  this.getLatLng = function (address) {
    if (address === "Amsterdam") {
      return "52.3700° N, 4.8900° E";
    } else if (address === "London") {
      return "51.5171° N, 0.1062° W";
    } else if (address === "Paris") {
      return "48.8742° N, 2.3470° E";
    } else if (address === "Berlin") {
      return "52.5233° N, 13.4127° E";
    } else {
      return "";
    }
  };
}

function GeoProxy() {
  var geocoder = new GeoCoder();
  var geocache = {};

  return {
    getLatLng: function (address) {
      if (!geocache[address]) {
        geocache[address] = geocoder.getLatLng(address);
      }
      console.log(address + ": " + geocache[address]);
      return geocache[address];
    },
    getCount: function () {
      var count = 0;
      for (var code in geocache) {
        count++;
      }
      return count;
    },
  };
}

function run() {
  var geo = new GeoProxy();

  // geolocation requests

  geo.getLatLng("Paris");
  geo.getLatLng("London");
  geo.getLatLng("London");
  geo.getLatLng("London");
  geo.getLatLng("London");
  geo.getLatLng("Amsterdam");
  geo.getLatLng("Amsterdam");
  geo.getLatLng("Amsterdam");
  geo.getLatLng("Amsterdam");
  geo.getLatLng("London");
  geo.getLatLng("London");

  console.log("\nCache size: " + geo.getCount());
}
```
