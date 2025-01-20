# 인증(Authentication) vs 인가(Authorization)

## 인증(Authentication)

- 정의: 누군가가 자신이 주장하는 사람인지 확인하는 과정
- 목적: 사용자의 신원을 확인
- 어떻게?:
  - 사용자 이름 + 비밀번호
  - 생체인증(지문, 얼굴 인식 등)
  - OTP(One-Time Password)
  - 결과: "이 사람이 맞아?"에 대한 답변
 
## 인가(Authorization)

- 정의: 인증된 사용자가 시스템에서 어떤 리소스에 접근할 권한이 있는지 확인하는 과정
- 목적: 권한 부여
- 어떻게?:
  - 역할(Role) 기반 접근 제어 (RBAC)
  - 권한 리스트
  - 정책 기반 접근 제어
  - 결과: "이 사람이 이걸 할 수 있어?"에 대한 답변
 
## HTTP Status Code

- 인증 실패: 401 Unauthorized
- 인가 실패: 403 Forbidden
