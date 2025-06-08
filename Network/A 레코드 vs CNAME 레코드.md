# A 레코드(Address Record) vs CNAME(Canonical Name) 레코드

도메인(DNS)을 구성하는 요소

## A 레코드

```
example.com.   A   192.0.2.1
```

- 도메인 -> IP 주소 직접 매핑
- 사용자가 example.com에 접속하면 브라우저는 바로 192.0.2.1로 연결됨

## CNAME 레코드

```
www.example.com.   CNAME   example.com.
```

- www.example.com을 요청하면 -> example.com을 요청하듯 동작함
- 최종 IP는 example.com의 A 레코드를 따라가게 됨

## 차이점 요약

| 항목        | A 레코드    | CNAME 레코드                               |
| --------- | -------- | --------------------------------------- |
| 매핑 대상     | IP 주소    | 다른 도메인 이름                               |
| 목적        | 도메인 -> IP | 도메인 -> 도메인(별칭)                          |
| IP 직접 지정  | ✅ 가능     | ❌ 불가능                                   |
| 루트 도메인 사용 | ✅ 가능     | ❌ 보통 안 됨(`example.com`에 CNAME은 권장 안 함) |

## 예시

```
example.com.         A       93.184.216.34
www.example.com.     CNAME   example.com.
```

- www.example.com은 -> example.com을 따라감 -> 결과적으로 93.184.216.34로 연결됨

## 사용 이유

### 1. 유지보수가 쉬움(중앙 집중식 관리)

```
app.example.com     CNAME   main.example.com
blog.example.com    CNAME   main.example.com
```

- 이때 main.example.com의 A 레코드만 바꾸면 모든 서브도메인이 한꺼번에 갱신됨

### 2. 외부 서비스와 연동할 때 필수적인 경우 많음

```
myapp.com       CNAME   myapp.netlify.app
```

- GitHub Pages, Netlify, AWS CloudFront, Firebase Hosting 등의 서비스는 고정 IP를 제공하지 않고, something.example.net 같은 도메인 형태의 엔드포인트를 제공
- 이 경우엔 A 레코드로는 연결 불가 -> CNAME 필수

### 3. Alias 역할(별칭 주소 제공)

```
www.example.com     CNAME   example.com
```

- www.example.com -> example.com 같이 사용자 편의성을 위해 도메인을 다양하게 alias 처리할 때 유용
- 사용자는 어떤 주소로 접속하든 같은 사이트로 이동 가능

### 4. IPv6 등 다른 레코드와 조합

- A 레코드는 IPv4만 지원
- 만약 IPv6(A 레코드는 못함) 주소도 써야 한다면 -> AAAA, CNAME 등을 조합해서 관리가 쉬워짐
