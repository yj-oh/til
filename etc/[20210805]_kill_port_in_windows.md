# Windows10 사용 중인 포트 죽이기
- 어쩌다 윈도우로 다시 돌아옴. 버벅버벅.

## 특정 포트 PID 확인
```text
netstat -ano | findstr {port_number}
```
- 그럼 19001 이런 식으로 숫자가 나옴. 걔가 PID

## 죽어라
```text
taskkill /f /pid {PID}
```
