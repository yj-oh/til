# MySQL root 비밀번호 리셋 (Windows)

## 상황
- [설치하고 환경변수 설정하고,]([20210720]_adding_mysql_to_path_env_variable_in_windows.md) 
  cmd에 `mysql -u root -p` 입력하고 초기 비밀번호 설정 안 했으니
  비밀번호 입력하라는 명령줄에 입력 없이 엔터키 눌렀는데 접속을 못함.
- MySQL 서버 시작해줘야 하는데 `mysql.server start` 명령어 못 씀.
  - `윈도우키 + R` - `services.msc` 입력 후 엔터 - mysql 찾아서 오른쪽 버튼 클릭 - 시작
- 다시 `mysql -u root -p`. 이번에는 
    ```
    ERROR 1045 (28000): access denied for user 'root'@'localhost' (using password: NO)
    ```
- root 비밀번호를 초기화 하기로 한다.

## root 비밀번호 초기화
- `윈도우키 + R` - `services.msc` 입력 후 엔터 - mysql 찾아서 오른쪽 버튼 클릭 - 중지
- cmd 관리자 권한으로 실행
  ```text
  mysqld --skip-grant-tables
  ```
- 그럼 아래와 같이 먹통인 것처럼 보인다.

![](.%5B20210721%5D_reset_mysql_root_password_images/497b14a4.png)

- 새로운 cmd 관리자 권한으로 실행
- 비밀번호 없이 접속
  ```text
  mysql -u root
  ```
- 비밀번호 변경
```text
use mysql;
```
```text
// >= 5.7
update user set authentication_string=password('{password}') where user='root';

// < 5.7
update mysql.user set password=password('{password}') where user='root';
```
- `{password}`에 변경할 비밀번호 입력한다.
```text
flush privileges;
quit
```
- `윈도우키 + R` - `services.msc` 입력 후 엔터 - mysql 찾아서 오른쪽 버튼 클릭 - 시작
