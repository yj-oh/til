# Keycloak - create user 권한 설정

## Get started
##### https://www.keycloak.org/getting-started/getting-started-zip
- .zip 다운로드
- 압축 해제하고 디렉토리로 이동
- run
    ```bash
    bin/standalone.sh
    ```
  
## Settings
##### http://localhost:8080
- admin 계정 생성 \
![http://localhost:8080/auth/](.%5B20200926%5D_keycloak_create_user_권한_images/01.png)

- add realm \
![http://localhost:8080/auth/admin/master/console/#/realms/master](.%5B20200926%5D_keycloak_create_user_권한_images/146bcade.png)
![http://localhost:8080/auth/admin/master/console/#/create/realm](.%5B20200926%5D_keycloak_create_user_권한_images/9bbe6617.png)

- create clients \
![http://localhost:8080/auth/admin/master/console/#/realms/test/clients](.%5B20200926%5D_keycloak_create_user_권한_images/sdf8338df.png)
![http://localhost:8080/auth/admin/master/console/#/create/client/test](.%5B20200926%5D_keycloak_create_user_권한_images/d9bfd9f3.png)

- client 설정 \
![http://localhost:8080/auth/admin/master/console/#/create/client/test](.%5B20200926%5D_keycloak_create_user_권한_images/sdf8338dg.png) \
*ㄴ 하단 save 버튼 클릭* \
![http://localhost:8080/auth/admin/master/console/#/create/client/test](.%5B20200926%5D_keycloak_create_user_권한_images/00005.png) \
*ㄴ `client_secret` 기억*

- client - add role \
![http://localhost:8080/auth/admin/master/console/#/realms/test/clients/](.%5B20200926%5D_keycloak_create_user_권한_images/99b96b04.png) \
*ㄴ 우측 `Add Role` 버튼 클릭* \
![http://localhost:8080/auth/admin/master/console/#/create/role/test/clients/](.%5B20200926%5D_keycloak_create_user_권한_images/840c60d1.png)

- Roles \
![http://localhost:8080/auth/admin/master/coZnsole/#/realms/test/roles](.%5B20200926%5D_keycloak_create_user_권한_images/00006.png)
![http://localhost:8080/auth/admin/master/console/#/create/role/test](.%5B20200926%5D_keycloak_create_user_권한_images/c71716e9.png)
![https://keycloak.huray.io/auth/admin/master/console/#/realms/minus-test/roles](.%5B20200926%5D_keycloak_create_user_권한_images/00007.png)
![http://localhost:8080/auth/admin/master/console/#/realms/test/roles/{}](.%5B20200926%5D_keycloak_create_user_권한_images/00008.png)
