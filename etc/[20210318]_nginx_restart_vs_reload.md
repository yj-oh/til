# Nginx restart vs reload

## restart
- shutdown 후 재기동
- 설정 파일에 문법적 에러가 있을 경우 재기동되지 않음 (서버 죽음)
```
service nginx restart
```

## reload
- shutdown 없이 새 설정 파일을 불러와 적용
- 설정 파일에 문법적 에러가 있을 경우 새 설정이 적용되지 않음 (서버 살아있음)
- 단순 설정 파일 적용이라면 서버 중단 없이 reload 만으로 가능
```
nginx -s reload
```

### 💡 -s signal
- Send signal to a master process
  - stop : 즉시 종료
  - quit : 연결 중인 커넥션 모두 완료될 때까지 기다린 후 종료
  - reopen
  - reload

## 문법적 에러 확인
- 기동하지 않고 설정 파일의 온전성 점검
```
nginx -t
```
