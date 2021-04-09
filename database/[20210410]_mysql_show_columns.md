# MySQL 컬럼 정보 조회
- DB 툴을 사용하고 있지만 쿼리로 컬럼 구조를 조회하고 싶을 때가 있다.

```sql
SHOW COLUMNS FROM item_category;
```
```sql
DESC item_category;
```
![](.%5B20210410%5D_mysql_show_columns_images/83a1d758.png)

- comment, collation 등의 정보까지 조회하고 싶다면.
```sql
SHOW FULL COLUMNS FROM item_category;
```
![](.%5B20210410%5D_mysql_show_columns_images/df0a6fca.png)
