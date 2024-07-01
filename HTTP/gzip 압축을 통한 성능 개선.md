## gzip이란?

GNU zip의 준말이며, 유닉스에서 태어는 오픈소스 압축 프로그램을 의미한다. 알집이나 7zip에서 사용하는 것과 동일한 Deflate 압축 알고리즘을 사용한다.

## gzip을 사용한 텍스트 압축

gzip은 텍스트 압축을 하는데 있어 최상을 성능을 나타내는 것으로 알려져 있다. 우리의 웹사이트는 이미지를 제외한 대부분이 텍스트 컨텐츠로 구성되어 있기 때문에, HTTP 리소스를 압축하는데 적합하다.(CSS, JS, JSON 등)

또한 우리가 사용하는 대부분의 브라우저는 gzip 압축 프로그램을 내장하고 있으며, gzip으로 압축된 파일을 자동으로 해제하는 기능도 탑재하고 있다. 즉, 서버에서 gzip으로 압축된 형태의 리소스를 다운로드 받으면 자동으로 압축을 해제하여 사용한다.

> 사실 gzip 인코딩 기능은 HTTP/1.1 명세에 포함되어 있으며, HTTP/1.1 을 지원하는 대부분의 현재의 브라우저는 gzip 으로 압축된 콘텐츠를 사용 가능하다.

## gzip으로 압축된 리소스

HTTP 응답의 `Response Headers` 중 `Content-Encoding`의 값이 `gzip`으로 설정된 경우 정상적으로 gzip 압축된 리소스이다.

```
cache-control: no-cache,s-maxage=10
content-encoding: gzip
content-type: application/json
date: Mon, 15 Aug 2022 10:12:39 GMT
etag: W/"c8aa840b54e63b81c43df6fa3c793dc6"
last-modified: Fri, 12 Aug 2022 06:30:18 GMT
server: AmazonS3
vary: Accept-Encoding
```

크롬 개발자 도구의 `Network -> 설정 -> Use large request rows`를 활성화 하면 각 요청별 실제 사이즈와 압축되어 전송된 사이즈를 같이 볼 수 있다.

## gzip의 단점

gzip 압축을 위한 컴퓨팅 자원으로 인해 서버의 CPU와 메모리 사용량이 증가한다. 네트워크 대역폭에서 이득을 얻는 대신 서버 자원을 조금 더 사용하게 되는 셈이다.
