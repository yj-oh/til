# MySQL emoji 저장
- db에 emoji를 저장하려면 character set을 `utf8mb4`로 설정

## Database 설정
```mysql
CREATE DATABASE db_name CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;
```
```sql
ALTER DATABASE db_name CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;
```

## Table 설정
```mysql
CREATE TABLE table_name (
-- ...
) ENGINE = InnoDB DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_general_ci;
```

## CHARACTER SET 확인
#### Database
```mysql
SELECT default_character_set_name, DEFAULT_COLLATION_NAME 
  FROM information_schema.SCHEMATA
WHERE schema_name = db_name;
```

#### Table
```mysql
SELECT CCSA.character_set_name
  FROM information_schema.`TABLES` T,
       information_schema.`COLLATION_CHARACTER_SET_APPLICABILITY` CCSA
 WHERE CCSA.collation_name = T.table_collation
   AND T.table_name = table_name;
```

#### Column
```mysql
SHOW FULL COLUMNS FROM table_name;
```
