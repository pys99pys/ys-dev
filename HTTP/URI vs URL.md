# URI vs URL

## URI(Uniform Resource Identifier)

- URI는 자원을 식별하는 데 사용되는 문자열
- 자원의 위치(URL)나 이름(URN) 또는 둘 다 포함할 수 있음
- 모든 URL은 URI지만, 모든 URI가 URL인 것은 아님

### 예시

- URL:
  - https://www.example.com/index.html
  - 자원의 위치를 명확히 나타냄
- URN:
  - urn:isbn:978-3-16-148410-0
  - 자원의 이름을 식별, 위치 정보는 포함하지 않음

## URL(Uniform Resource Locator)

- URL은 자원의 위치를 나타내는 URI의 하위 집합
- 자원이 어디에 있는지(프로토콜 + 경로)를 명시적으로 가리킴

### 구성 요소

- 프로토콜: 리소스에 접근하는 방법(예: http, https, ftp)
- 호스트명: 리소스가 위치한 서버(예: www.example.com)
- 경로: 서버 내 리소스의 위치(예: /index.html)
- 쿼리 문자열 (선택적): 추가 파라미터(예: ?id=123)

## 차이점

- 포괄성:
  - URI는 URL과 URN을 모두 포함하는 상위 개념
  - URL은 URI 중 위치 정보를 나타내는 하위 개념
- 위치와 이름:
  - URI는 자원을 "식별"하는 모든 방법을 포함
  - URL은 자원의 "위치"를 구체적으로 나타냄
