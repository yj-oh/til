# MySQL 8.x 유저 비밀번호 변경
* 참고 : [MySQL 유저, 권한]([20200902]_mysql_user.md)

---

## MySQL console 접속
```
$ mysql -u root -p
password: 
```

## user 조회
```
$ SELECT host, user FROM mysql.user;
```

## 비밀번호 변경
```
$ alter user 'root'@'localhost' identified with mysql_native_password by '';
```

## 적용
```
flush privileges;
```
