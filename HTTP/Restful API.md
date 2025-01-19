# Restful API

REST(Representational State Transfer) 원칙에 기반을 둔 웹 서비스 아키텍처 스타일을 따르는 API

## 특징

### 자원(Resource) 기반

- 모든 데이터는 "자원"으로 간주되고, 각 자원은 고유한 URI를 가짐
- 예:
  - https://api.example.com/users/123 -> 특정 사용자 리소스
  - https://api.example.com/products -> 제품 목록 리소스

### HTTP 메서드 사용

- CRUD 작업(Create, Read, Update, Delete)에 HTTP 메서드를 매핑해서 사용
- GET: 데이터 조회
- POST: 새로운 데이터 생성
- PUT: 데이터 전체 수정
- PATCH: 데이터 부분 수정
- DELETE: 데이터 삭제

### 상태 무결성(Stateless)

- 서버는 클라이언트의 상태를 저장하지 않음
- 각 요청은 독립적으로 처리되며, 필요한 모든 정보는 요청에 포함되어야 함

### HTTP 상태 코드 활용

- 서버는 요청에 대한 결과를 HTTP 상태 코드로 전달
- 200 OK: 요청 성공
- 201 Created: 리소스 생성 성공
- 400 Bad Request: 잘못된 요청
- 404 Not Found: 리소스를 찾을 수 없음
- 500 Internal Server Error: 서버 오류

## 장점

- 단순하고 직관적: URI와 HTTP 메서드로 작업을 명확히 표현
- 확장성: 독립적인 자원 단위로 설계돼 추가 기능 확장이 쉬움
- 유연성: JSON, XML 등 다양한 데이터 형식을 지원
- 플랫폼 독립성: HTTP와 표준 기술을 사용해 클라이언트와 서버 간 통신
