# MySQL 전체 데이터 수 확인
```mysql
SELECT SUM(TABLE_ROWS) -- TABLE_NAME, TABLE_COMMENT, TABLE_ROWS
  FROM INFORMATION_SCHEMA.TABLES
 WHERE TABLE_SCHEMA = 'okky'
 ORDER BY TABLE_ROWS DESC
```