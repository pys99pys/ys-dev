# Stale-While-Revalidate, Stale-If-Error Header

## stale-while-revalidate

오리진에서 객체를 응답하는 동안 비동기적으로 캐시된 객체를 제공

```
Cache-Control: max-age=3600, stale-while-revalidate=600
```

위 설정은 3600초간 캐시된 객체를 제공, 그 이후에는 600초간 캐시 됐던 리소스를 제공하는 동시에 캐시된 객체를 새로고침 하라는 요청을 전송

## stale-if-error

오리진 객체가 에러 응답을 하는 경우 캐시된 객체를 제공

```
Cache-Control: max-age=3600, stale-if-error=86400
```

위 설정은 3600초간 캐시된 객체를 제공, 그 이후에는 오리진 객체에서 에러 발생시 86400초간 캐시 됐던 리소스를 제공
