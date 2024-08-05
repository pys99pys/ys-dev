다음을 모두 만족하지 않으면 preflight가 발생(simple request가 아닌 경우)
- GET, HEAD, POST 요청
- 자동으로 설정되는 헤더 외에 Accept, Accept-Language, Content-Language, Content-Type 헤더의 값만 수동으로 설정 가능
- Content-Type 헤더는 application/x-www-form-urlencoded, multipart/form-data, text/plain만 허용
- 요청에 사용된 XMLHttpRequest.upload 객체에 이벤트 리스너가 등록되어 있지 않을 때
- ReadableStream 객체가 요청에서 사용되지 않을 때
