# EC2 instance SSH 접속 - Permission denied error

#### 접속 시도
```
ssh -i file.pem ec2-user@IP
```

#### 에러
```
WARNING: UNPROTECTED PRIVATE KEY FILE!

bad permissions: ignore key: amazonec2.pem
Permission denied (publickey).
```

#### 해결
```
chmod 400 file.pem
```

### 👉 `chmod`
- 파일 또는 디렉토리 권한 변경

###  👉 접근 권한에 대한 8진수 값
# | Permission | rwx | Binary
--- | --- | --- | ---
7 | read, write and execute	| rwx | 111
6 | read and write | rw- | 110
5 | read and execute | r-x | 101
4 | read only | r-- | 100
3 | write and execute | -wx | 011
2 | write only | -w- | 010
1 | execute only | --x | 001
0 | none | --- | 000

##### * Reference : https://en.wikipedia.org/wiki/Chmod
