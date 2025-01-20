# withCredentials

XMLHttpRequest 또는 Fetch API에서 사용되는 속성으로, 요청에 쿠키, 인증 헤더 또는 기타 자격 증명을 포함할지를 결정

## 사용법

**XMLHttpRequest**

```
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://example.com', true);
xhr.withCredentials = true; // 자격 증명 포함
xhr.send();
```

**Fetch API**

```
fetch('https://example.com', {
  credentials: 'include', // 자격 증명 포함
});
```

## 주요 값

- same-origin: 동일 출처에만 자격 증명 포함(기본값, Fetch API에서 사용)
- include: 모든 요청에 자격 증명 포함
- omit: 자격 증명을 포함하지 않음

## 주의사항

- 서버는 응답 헤더에 Access-Control-Allow-Credentials: true를 설정해야 함
- CORS 요청에서 자격 증명을 포함하면 보안상 위험이 증가할 수 있으므로 신중히 사용해야 함
