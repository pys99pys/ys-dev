# HTTP 헤더

HTTP 헤더는 요청(request)이나 응답(response)에 부가적인 정보를 담는 역할

## 요청 헤더(Request Header)

| 헤더 | 설명 |
|------|------|
| `Host` | 요청 대상 서버의 도메인 (예: `Host: example.com`) |
| `User-Agent` | 요청을 보낸 클라이언트 정보 (브라우저, OS 등) |
| `Accept` | 클라이언트가 받을 수 있는 MIME 타입 (`Accept: application/json`) |
| `Accept-Language` | 선호하는 언어 (`Accept-Language: ko-KR`) |
| `Content-Type` | 요청 본문의 데이터 타입 (`application/json`, `multipart/form-data` 등) |
| `Authorization` | 인증 정보 (예: `Bearer <token>`) |
| `Cookie` | 클라이언트가 보유한 쿠키 전달 |

## 응답 헤더(Response Header)

| 헤더 | 설명 |
|------|------|
| `Content-Type` | 응답 데이터의 타입 (예: `text/html`, `application/json`) |
| `Set-Cookie` | 클라이언트에게 쿠키를 설정하도록 지시 |
| `Cache-Control` | 캐싱 정책 (`no-store`, `max-age=3600` 등) |
| `Location` | 리디렉션 주소 (3xx 응답 시 사용) |
| `Access-Control-Allow-Origin` | 허용된 도메인(origin) 설정 (CORS 관련) |
| `Access-Control-Allow-Headers` | 클라이언트가 보낼 수 있는 헤더 목록 (CORS) |
| `Content-Length` | 응답 본문의 바이트 크기 |

## 보안 관련 헤더(Security Header)

| 헤더 | 설명 |
|------|------|
| `Strict-Transport-Security` | HTTPS 연결 강제 (HSTS) |
| `X-Content-Type-Options` | MIME 타입 추측 방지 (`nosniff`) |
| `X-Frame-Options` | iframe 내 삽입 방지 (`DENY`, `SAMEORIGIN`) |
| `Content-Security-Policy` | 리소스 로딩 및 스크립트 실행 제어 정책 |
| `Referrer-Policy` | Referer 헤더 노출 제어 |
| `Permissions-Policy` | 카메라, 마이크, 위치 등 브라우저 기능 사용 제어 |
