## MySQL console 접속
```
$ mysql -u root -p
password: 
```

## user 조회
```
$ SELECT host, user FROM mysql.user;
```

## user 생성
```
$ CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```
- 외부 접근 권한을 주려면 host를 '%'로 설정
```
$ CREATE USER 'username'@'%' IDENTIFIED BY 'password';
```

## user 삭제
```
$ DROP USER 'username'@'host';
```

## 권한 조회
```
$ SHOW GRANTS FOR 'username'@'host';
```

## 권한 부여
```
$ GRANT ALL PRIVILEGES ON 'db name'.* TO 'username'@'host';
```
- ex) `GRANT ALL PRIVILEGES ON test.* TO test_user@localhost;`
   - → `test_user` 유저에게 `test` 데이터베이스에 대한 모든 권한 부여
   
권한 | 설명 
--- | ---
ALL PRIVILEGES | as we saw previously, this would allow a MySQL user full access to a designated database (or if no database is selected, global access across the system)
CREATE | allows them to create new tables or databases
DROP | allows them to them to delete tables or databases
DELETE | allows them to delete rows from tables
INSERT | allows them to insert rows into tables
SELECT | allows them to use the SELECT command to read through databases
UPDATE | allow them to update table rows
GRANT OPTION | allows them to grant or remove other users’ privileges
- Reference : https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql

## 권한 적용
```
$ FLUSH PRIVILEGES;
```
