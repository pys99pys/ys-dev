# JWT(JSON Web Token)

클라이언트와 서버 간의 안전하고 간편한 데이터 교환을 위한 토큰 기반 인증 기술

## 구조

JWT는 세 부분으로 나뉘며, 각 부분은 Base64Url 인코딩으로 인코딩됨

### 헤더(Header)

- JWT의 타입과 해싱 알고리즘 정보를 담고 있음

```
{
  "alg": "HS256", // 해싱 알고리즘 (HMAC-SHA256)
  "typ": "JWT"    // 타입: JWT
}
```

### 페이로드(Payload)

- JWT에 저장할 데이터를 담는 부분으로, **클레임(Claim)**이라고 불림
- 클레임은 세 가지 유형으로 나뉨
  - 등록된 클레임: 표준으로 정의된 필드(예: iss, exp, sub, aud).
  - 공개 클레임: 애플리케이션에서 자유롭게 정의
  - 비공개 클레임: 클라이언트와 서버 간에만 사용하는 정보
 
```
{
  "sub": "1234567890",    // 사용자 ID
  "name": "John Doe",    // 사용자 이름
  "iat": 1516239022      // 토큰 발행 시간
}
```

### 서명(Signature)

- 데이터 위변조를 방지하기 위한 서명
- 서명 생성 방식
- 이 서명은 비밀 키(secret)를 사용해 생성되며, 서버가 이 서명을 검증함으로써 토큰의 무결성을 확인

```
Signature = HMACSHA256(
  Base64UrlEncode(Header) + "." + Base64UrlEncode(Payload),
  secret
)
```

## 예시

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

**Header: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9**

```
{"alg": "HS256", "typ": "JWT"}
```

**Payload: eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ**

```
{"sub": "1234567890", "name": "John Doe", "iat": 1516239022}
```

**Signature: SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c**

## 장점

- 독립적이고 자체 포함적
  - JWT는 필요한 모든 정보를 포함하므로 서버가 별도의 세션 상태를 유지하지 않아도 됨
- 확장성과 분산 아키텍처에 적합
  - 서버 간 상태 공유가 필요 없는 무상태 인증
- 간편한 데이터 전송
  - Base64Url로 인코딩되어 JSON 데이터를 간편하게 전송 가능
- 다양한 용도
  - 인증(Authorization): 로그인 상태 유지
  - 데이터 교환(Data Exchange): 서버 간 안전한 데이터 전송
 
## 단점

- 크기 문제
  - Base64Url 인코딩으로 인해 텍스트 크기가 다소 커질 수 있음
- 유효 기간 관리
  - 토큰이 클라이언트에 저장되므로 만료 전까지는 회수 불가, 따라서 민감한 정보가 담긴 JWT는 조심히 사용해야 함
- 보안 위험
  - 토큰이 클라이언트에 저장되므로, 탈취 시 부적절한 접근 가능
  - 비밀 키 관리 및 HTTPS 사용이 필수
