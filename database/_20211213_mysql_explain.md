# MySQL 실행계획
- 실행계획을 보려면 쿼리 앞에 `EXPLAIN` 키워드를 사용한다.
```mysql
EXPLAIN 
SELECT *
  FROM table_name
```
- 아래 내용은 [MySQL docs - 8.8.2 EXPLAIN Output Format](https://dev.mysql.com/doc/refman/8.0/en/explain-output.html) 를 참고하여 정리했다.

---

# EXPLAIN Output Columns
| Column                           | Meaning             |
|----------------------------------|---------------------|
| [id](#-id)                       | `SELECT` id         |
| [select_type](#-select_type)     | `SELECT` type       |
| [table](#-table)                 | 참조하는 table          |
| [partitions](#-partitions)       | 파티셔닝                |
| [type](#-type)                   | join type           |
| [possible_keys](#-possible_keys) | 선택 가능한 index        |
| [key](#-key)                     | 실제 선택된 index        |
| [key_len](#-key_len)	            | 실제 선택된 index의 길이    |
| [ref](#-ref)	                    | index 와 비교하는 column |
| [rows](#-rows)                   | 검사할 행의 추정치          |
| [filtered](#-filtered)           | WHERE 조건 적용 후의 행    |
| [extra](#-extra)                 | 추가 정보               |

## 👉 id
- `SELECT` 식별자.
- SUB QUERY, UNION 이 없으면 `SELECT`는 하나뿐이므로 항상 `1`이 된다.
- `SELECT`가 여러 개일 경우 순차적으로 번호가 매겨진다.

## 👉 select_type
| select_type Value    | Meaning                                        |
|----------------------|------------------------------------------------|
| SIMPLE               | 단순 SELECT (UNION, SUB QUERY 가 없음)              |
| PRIMARY              | UNION 의 첫번째 SELECT, SUB QUERY 의 외부 SELECT      |
| UNION                | UNION 의 PRIMARY 이후 SELECT                      |
| DEPENDENT UNION      | UNION 의 PRIMARY 이후 SELECT, 외부 쿼리에 의존적          |
| UNION RESULT         | UNION 의 결과                                     |
| SUBQUERY             | 서브 쿼리의 첫 번째 SELECT                             |
| DEPENDENT SUBQUERY   | 서브 쿼리의 첫 번째 SELECT, 외부 쿼리에 의존적                 |
| DERIVED              | FROM 절에 서브쿼리로 만들어진 테이블, 임시적으로 생성되는 서브 쿼리, VIEW |
| DEPENDENT DERIVED    | 다른 테이블에 종속된 Derived table                      |
| MATERIALIZED         | IN 절의 서브 쿼리를 임시 테이블로 만들어 최적화                   |
| UNCACHEABLE SUBQUERY | 캐싱 불가능한 SUBQUERY                               |
| UNCACHEABLE UNION    | 캐싱 불가능한 UNION                                  |

## 👉 table
- 접근하는 테이블

## 👉 partitions
- 파이셔닝 되어있는 테이블의 경우 값이 들어감.

## 👉 type
- 테이블의 join 방법 유형
- 아래로 갈수록 구린 유형이다.

| type Value                          | Meaning                                                                                                                                          |
|-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| system                              | 테이블에 하나의 데이터만 있을 때                                                                                                                               |
| [const](#const)                     | PRIMARY KEY 또는 UNIQUE 인덱스 활용. 최대 한 건의 일치하는 행이 있다. 빠름.                                                                                            |
| [eq_ref](#eq_ref)                   | PRIMARY KEY 또는 UNIQUE NOT NULL 인덱스 활용하여 하나의 데이터를 선택. <br/> `=` 연산자로 비교하는 인덱싱 컬럼에 사용                                                              |
| [ref](#ref)                         | KEY 의 최좌측 prefix 만 사용하거나 PRIMARY KEY 또는 UNIQUE 인덱스가 아닌 경우(조인이 키 값으로 단일 행을 선택할 수 없을 때). 키가 몇 개의 행과 일치하는 경우. <br/> `=`, `<=>` 연산자로 비교하는 인덱싱 컬럼에 사용 |
| fulltext                            | FULLTEXT 인덱스를 사용하여 조인                                                                                                                            |
| [ref_or_null](#ref_or_null)         | ref 와 유사하지만 NULL 값을 포함하는 행에 대한 추가 검색.                                                                                                            |
| index_merge                         | 2개 이상의 인덱스를 이용해 결과를 만들고 합친다.                                                                                                                     |
| [unique_subquery](#unique_subquery) | WHERE 조건절에 사용되는 IN 의 서브쿼리가 PRIMARY KEY 를 반환.                                                                                                     |
| [index_subquery](#index_subquery)   | unique_subquery 와 유사하지만 서브쿼리가 유니크하지 않은 INDEX 를 반환.                                                                                               |
| [range](#range)                     | 지정된 범위 내에서 인덱스를 사용하여 검색. <br/> =, <>, >, >=, <, <=, IS NULL, <=>, BETWEEN, LIKE, or IN()                                                         |
| index                               | 인덱스 풀스캔                                                                                                                                          |
| all                                 | 테이블 풀스캔                                                                                                                                          |

### const
- PRIMARY KEY 또는 UNIQUE 인덱스 활용. 최대 한 건의 일치하는 행이 있다. 빠름.
```mysql
SELECT * 
  FROM tbl_name 
 WHERE primary_key = 1;

SELECT * FROM tbl_name
 WHERE primary_key_part1 = 1 
   AND primary_key_part2 = 2;
```

### eq_ref
- PRIMARY KEY 또는 UNIQUE NOT NULL 인덱스 활용하여 하나의 데이터를 선택.
- `=` 연산자로 비교하는 인덱싱 컬럼에 사용
```mysql
SELECT * 
  FROM ref_table,other_table
 WHERE ref_table.key_column = other_table.column;

SELECT * 
  FROM ref_table,other_table
 WHERE ref_table.key_column_part1 = other_table.column
   AND ref_table.key_column_part2 = 1;
```

### ref
- KEY 의 최좌측 prefix 만 사용하거나 PRIMARY KEY 또는 UNIQUE 인덱스가 아닌 경우(조인이 키 값으로 단일 행을 선택할 수 없을 때). 
- 키가 몇 개의 행과 일치하는 경우.
- `=`, `<=>` 연산자로 비교하는 인덱싱 컬럼에 사용
```mysql
SELECT * 
  FROM ref_table 
 WHERE key_column = expr;

SELECT * 
  FROM ref_table,other_table
  WHERE ref_table.key_column = other_table.column;

SELECT * 
  FROM ref_table,other_table
 WHERE ref_table.key_column_part1 = other_table.column
   AND ref_table.key_column_part2 = 1;
```

### ref_or_null
- ref 와 유사하지만 NULL 값을 포함하는 행에 대한 추가 검색.
```mysql
SELECT * 
  FROM ref_table
 WHERE key_column = expr 
    OR key_column IS NULL;
```

### unique_subquery
- WHERE 조건절에 사용되는 IN 의 서브쿼리가 PRIMARY KEY 를 반환.
```mysql
value IN (SELECT primary_key FROM single_table WHERE some_expr)
```

### index_subquery
- unique_subquery 와 유사하지만 서브쿼리가 유니크하지 않은 INDEX 를 반환.
```mysql
value IN (SELECT key_column FROM single_table WHERE some_expr)
```

### range
- 지정된 범위 내에서 인덱스를 사용하여 검색.
- =, <>, >, >=, <, <=, IS NULL, <=>, BETWEEN, LIKE, or IN()
```mysql
SELECT * 
  FROM tbl_name
 WHERE key_column = 10;

SELECT * 
  FROM tbl_name
 WHERE key_column BETWEEN 10 and 20;

SELECT * 
  FROM tbl_name
 WHERE key_column IN (10, 20, 30);

SELECT * 
  FROM tbl_name
 WHERE key_part1 = 10 
   AND key_part2 IN (10, 20, 30);
```

## 👉 possible_keys
- 선택 가능한 후보 인덱스

## 👉 key
- possible_keys 중 실제 사용된 인덱스

## 👉 key_len
- 인덱스에 사용하고 있는 byte 수. 
- 인덱스 컬럼 중 일부만 사용한다면 이 컬럼 값을 이용해 사용되는 컬럼을 계산할 수 있다.

## 👉 ref
- 인덱스에서 값을 검색할 때 사용된 컬럼
- 함수로 가공된 컬럼 값이 사용되면 `func`

## 👉 rows
- 쿼리를 실행하기 위해 검사해야 하는 행의 수를 예측한 값
- InnoDB 테이블은 추정치이고 실제 값과 일치하지 않을 수 있다.

## 👉 filtered
- 테이블 조건으로 필터링 후 남은 행의 예상 백분율.
- 100 일 경우 필터링이 발생하지 않았음을 의미.

## 👉 extra
- [MySQL docs - EXPLAIN Extra Information](https://dev.mysql.com/doc/refman/8.0/en/explain-output.html#explain-extra-information)
