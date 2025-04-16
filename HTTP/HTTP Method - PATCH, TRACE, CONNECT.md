## HEAD

헤더만 요청할 때 사용, 멱등(idempotent) o, 안전(safe) o

## PATCH

리소스 부분 수정 요청시 사용, 멱등(idempotent) x, 안전(safe) x

## TRACE

요청 - 응답까지의 레이턴시에서 거친 프록시 서버를 알고싶을 때 사용, 멱등(idempotent) o, 안전(safe) o

## CONNECT

SSL 터널링 등 특수 용도에 사용, 멱등(idempotent) o, 안전(safe) o
