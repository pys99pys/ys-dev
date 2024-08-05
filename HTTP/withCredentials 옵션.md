## withCredentials 옵션?

크로스도메인 요성시 credential 정보를 포함할지 여부

- 쿠키를 포함한 요청
- Authorization 헤더를 포함한 요청

위 요청일 때는 반드시 `withCredentials: true`를 설정해줘야 함

## 서버 응답

credential 정보가 포함된 요청을 처리하기 위해 서버에서도 아래 응답값을 설정해주어야 함

- `Access-Control-Allow-Credentials: true`
- `Access-Control-Allow-Origin` 설정(와일드카드 허용x)
- `Access-Control-Allow-Methods` 설정(와일드카드 허용x)
- `Access-Control-Allow-Headers` 설정(와일드카드 허용x)
