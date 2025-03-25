# XSS(Cross-Site Scripting)

사용자가 입력한 스크립트(보통 자바스크립트)가 그대로 웹 페이지에 출력되어, 브라우저에서 실행되도록 만드는 공격 방식

## 예시

**코드**

```
<!-- 사용자의 닉네임을 표시 -->
<div>안녕하세요, <strong>{{ nickname }}</strong> 님!</div>
```

**사용자가 아래와 같이 입력**

```
<script>alert('해킹');</script>
```

**결과**

```
<div>안녕하세요, <strong><script>alert('해킹');</script></strong> 님!</div>
```

-> 이 코드는 브라우저에서 실제로 실행돼서 사용자 세션 탈취, 피싱, 악성 코드 삽입이 가능해짐

## 종류

- Stored XSS: 악성 스크립트가 DB에 저장돼 여러 사용자에게 노출됨
- Reflected XSS: 공격자가 만든 링크에 포함된 스크립트가 즉시 실행됨
- DOM-based XSS: 자바스크립트로 조작한 DOM에 악성 코드가 삽입됨

## 방어법

- 출력 시 이스케이프: <, >, " 같은 특수 문자 변환 (&lt;, &gt; 등)
- HTML 템플릿 엔진 사용: 자동으로 escape 처리되는 프레임워크 사용 (React, Vue 등)
- 콘텐츠 보안 정책(CSP): <script> 삽입을 제한하는 HTTP 헤더 설정
- 사용자 입력 검증: <script>, onerror 등 금지어 필터링
- DOM 조작 시 주의: innerHTML 대신 textContent, createElement 사용
