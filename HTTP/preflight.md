CORS(Cross-Origin Resource Sharing) 정책에 따라 브라우저가 서버에 실제 요청을 보내기 전에 HTTP OPTIONS 요청을 보내는 과정

이 요청은 주로 HTTP 헤더나 메서드가 표준적인 값이 아닌 경우에 발동되며, preflight 요청을 통해 서버가 해당 요청을 허용하는지 확인함

## Preflight 요청 발동 조건

1. 메서드(Method)
  - GET, POST, HEAD 외의 HTTP 메서드를 사용할 경우
  - 예: PUT, DELETE, PATCH 등의 메서드를 사용할 때

2. 헤더(Headers)
  - Content-Type이나 Authorization과 같은 특수한 헤더가 포함된 요청
  - 예: Content-Type: application/json, Authorization: Bearer ... 등과 같은 비표준 헤더가 포함될 때

3. 비표준 Content-Type
  - Content-Type이 기본값인 application/x-www-form-urlencoded, multipart/form-data, text/plain이 아닐 경우
  - 예: application/json, application/xml 등 비표준 Content-Type을 사용할 경우

4. 쿠키(Cookies)
  - 요청에 withCredentials 옵션이 포함되어 쿠키를 포함한 요청을 보내는 경우
  - 예: fetch나 XMLHttpRequest에서 withCredentials: true 옵션을 설정한 경우 
