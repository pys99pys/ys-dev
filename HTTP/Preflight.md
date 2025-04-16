# Preflight

브라우저가 본 요청을 보내기 전에, 미리 괜찮은 요청인지 물어보는 과정

## 필요한 이유

- 보안상의 이유로, 브라우저는 교차 출처 요청(Cross-Origin Request) 중 "민감하거나 비표준적인 요청"이면 그냥 보내지 않음
- 대신 먼저 OPTIONS 메서드로 "사전 요청(Preflight)"을 보내고, 서버가 OK 응답을 주면 진짜 요청을 보냄

## 발생 조건

아래 중 하나라도 만족하면 Preflight 요청 발생

1. 메서드가 GET, POST, HEAD가 아닌 경우(PUT, PATCH, DELETE 등)
2. Content-Type이 아래 중 하나가 아닌 경우:
  - application/x-www-form-urlencoded
  - multipart/form-data
  - text/plain
3. 커스텀 헤더가 있는 경우(ex. Authorization, X-Custom-Token 등)

## 예시

**프리플라이트 요청(브라우저가 자동으로 보냄)**

```
OPTIONS /api/user HTTP/1.1
Origin: https://frontend.com
Access-Control-Request-Method: PATCH
Access-Control-Request-Headers: Content-Type, Authorization
```

**서버 응답**

```
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://frontend.com
Access-Control-Allow-Methods: GET, POST, PATCH, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization
```

-> 이 응답을 보고 브라우저가 진짜 PATCH 요청을 보냄

## 최적화 팁

- 불필요한 프리플라이트 줄이기
  - 메서드: GET, POST 사용
  - 헤더: Content-Type을 application/x-www-form-urlencoded로 맞추기
  - 커스텀 헤더 최소화
- 서버에서 OPTIONS 요청에 대한 CORS 헤더를 캐시 설정(Access-Control-Max-Age) 해주면 성능 향상
