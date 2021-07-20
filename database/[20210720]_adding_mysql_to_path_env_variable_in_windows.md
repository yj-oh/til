# MySQL 환경변수 추가 (Windows)
- ~~윈도우 적응하느라 돌아버리겠다.~~

## 다운로드
- MySQL 다운로드
  - https://downloads.mysql.com/archives/installer/
- MariaDB 다운로드
  - https://downloads.mariadb.org/
    
## 환경변수 설정
- `윈도우키 + R` - `sysdm.cpl` 입력 후 엔터 - 고급 탭 - 환경변수
- 시스템 변수의 path 선택 - 편집

![](.%5B20210720%5D_adding_mysql_to_path_env_variable_in_windows_images/ac9311ee.png)

- 새로 만들기 - MySQL/MariaDB 설치한 폴더의 bin 폴더 경로 붙여넣기
  - e.g. `C:\Program Files\MariaDB 10.6\bin`

## 확인
- cmd에 `mysql --version` 또는 `mariadb --version`
- ✔ 기존에 켜놨던 cmd창 말고 새로운 창 켜서 해야 한다.
