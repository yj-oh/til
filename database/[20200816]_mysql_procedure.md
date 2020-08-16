# MySQL/MariaDB Procedure

## 👉 포맷
```mysql
DELIMITER $$
DROP PROCEDURE IF EXISTS {프로시저명}
CREATE PROCEDURE {프로시저명}
BEGIN
  -- 실행할 내용
END
```

## 👉 명령어
#### 프로시저 목록
```mysql
SHOW PROCEDURE STATUS;
```

#### 프로시저 스크립트 확인
```mysql
SHOW CREATE PROCEDURE {프로시저명};
```

#### 프로시저 호출
```mysql
CALL {프로시저명};
```

#### 프로시저 삭제
```mysql
DROP PROCEDURE {프로시저명};
```

#### 프로시저를 수정하고자 할 때에는 삭제하고 다시 생성


## 👉 예제
- 더미 데이터 99개 insert하는 프로시저
```mysql
DELIMITER $$
CREATE PROCEDURE loop_insert_data
BEGIN
    DECLARE id_data INT DEFAULT 1;
    DECLARE date_data DATETIME DEFAULT '2020-01-01 00:00:00';

    loop_xxxx:LOOP
        IF(id_data = 100) THEN
	        LEAVE loop_xxxx;
        END IF;
       INSERT INTO document (id, content, created_at)
       VALUES (id_data, '내용', date_data,);

        SET id_data = id_data + 1;
        SET date_data = ADDDATE(date_data, 1);
    END LOOP;
END
```

```mysql
DROP PROCEDURE IF EXISTS loop_insert_data
CREATE PROCEDURE loop_insert_data
```
→ `loop_insert_data`라는 프로시저가 있으면 삭제하고 생성

```mysql
BEGIN
END
```
→ 프로시저 시작과 끝

```mysql
DECLARE id_data INT DEFAULT 1;
DECLARE date_data DATETIME DEFAULT '2020-01-01 00:00:00';
```
→ 변수 선언 및 기본값 설정

```mysql
loop_xxxx:LOOP
END LOOP;
```
→ 루프 시작과 끝

```mysql
IF(id_data = 100) THEN
    LEAVE loop_xxxx;
END IF;
```
→ id_data가 100이 되면 루프 종료

```mysql
INSERT INTO document (id, content, created_at)
VALUES (id_data, '내용', date_data,);

SET id_data = id_data + 1;
SET date_data = ADDDATE(date_data, 1);
```
→ 루프를 돌며 데이터 insert, 변수 값 변경
