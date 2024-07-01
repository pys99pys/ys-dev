## 사용중인 포트의 PID 찾기

```
$ lsof -i :{PORT}
```

## 해당 PID를 kill 하기

```
$ kill -9 {PID}
```
