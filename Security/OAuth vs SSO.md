# OAuth(Open Authorization) vs SSO(Single Sign-On)

사용자 인증(Authentication)과 관련된 개념

## OAuth

주로 **"권한 위임(Authorization)"**을 위한 프로토콜로 특정 애플리케이션이 사용자의 자격 증명을 직접 다루지 않고도, 다른 서비스(예: Google, Facebook)에서 제공하는 리소스에 접근할 수 있도록 해 줌

### 주요 개념

- Access Token: 사용자가 인증되면 발급되는 토큰으로, 특정 리소스에 대한 접근 권한을 나타냄
- Refresh Token: Access Token이 만료될 경우 새 토큰을 요청할 수 있도록 해 줌
- Client: OAuth를 통해 권한을 요청하는 애플리케이션
- Resource Owner: 사용자의 리소스를 보호하는 주체(사용자 자신)
- Authorization Server: 권한을 인증하고 Access Token을 발급하는 서버
- Resource Server: 보호된 리소스를 제공하는 서버(예: Google Drive API)

### OAuth의 흐름(OAuth 2.0 기준)

- 사용자가 클라이언트 앱에서 로그인 버튼을 누름
- 클라이언트 앱이 **OAuth 제공자(예: Google, Facebook)**에게 권한을 요청
- 사용자가 로그인 및 권한을 승인하면 Authorization Server에서 Access Token을 발급
- 클라이언트 앱은 이 Access Token을 이용해 Resource Server(예: Google Drive)에서 데이터를 가져옴

### OAuth의 사용 예시

- "Google로 로그인" 버튼을 눌러 다른 웹사이트에 로그인(OAuth + OpenID Connect)
- 트위터에서 "Google Drive에 접근 권한 허용" 같은 기능

## SSO

하나의 로그인으로 여러 서비스에 접근할 수 있도록 해 주는 인증(Authentication) 방식으로 한 번 로그인하면 추가 인증 없이 다른 관련 서비스에도 접근할 수 있음

### 주요 개념

- Identity Provider(IdP): 사용자를 인증하고 SSO를 제공하는 서비스(예: Okta, Google Workspace, Microsoft Azure AD)
= Service Provider(SP): SSO를 통해 접근할 수 있는 애플리케이션(예: Gmail, Slack, Trello)
- Session Management: 한 번 로그인하면 같은 인증 정보로 다른 서비스도 이용할 수 있도록 유지

### SSO의 흐름

- 사용자가 **SSO 제공자(IdP)**에 로그인
- 인증이 완료되면 세션(Session)이 유지됨
- 사용자가 다른 서비스(SP)로 이동하면, 기존 로그인 정보를 기반으로 자동 인증됨

### SSO의 사용 예시

- Google Workspace(Gmail, Drive, Calendar 등 모든 Google 서비스에 한 번 로그인)
- 회사 내부의 여러 업무 시스템(예: Jira, Slack, Confluence 등)에서 SSO 사용
