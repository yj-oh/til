## jpa logging
### application.yml
```yaml
spring:
  jpa:
    database-platform: org.hibernate.dialect.MySQL5InnoDBDialect
    show-sql: true              # jpa가 생성하는 sql문을 출력
    properties:
      hibernate:
        format_sql: true        # sql문을 보기 좋게 정렬하여 출력
        use_sql_comments: true  # 추가적 정보 출력
logging:
  level:
    org.hibernate.type: trace   # 물음표로 표기된 bind parameter 값 출력
```

#### spring.jpa.show-sql=true
- jpa가 생성하는 sql문을 출력
```
Hibernate: select inputmethod0_.id as id1_3_0_, inputmethod0_.name as name4_3_0_, inputmethod0_.created_at as created_3_3_0_ from input_method inputmethod0_ where inputmethod0_.id=?
```

#### spring.jpa.properties.hibernate.format_sql=true
- sql문을 보기 좋게 정렬하여 출력
```
Hibernate: 
    select
        inputmethod0_.id as id1_3_0_,
        inputmethod0_.name as name4_3_0_,
        inputmethod0_.created_at as created_3_3_0_,
    from
        input_method inputmethod0_ 
    where
        inputmethod0_.id=?
```

#### spring.jpa.properties.hibernate.use_sql_comments=true
- 추가적 정보 출력
```
Hibernate: 
/* select
        generatedAlias0 
    from
        User as generatedAlias0 
    order by
        generatedAlias0.createdAt desc,
        generatedAlias0.id desc */ 
    select
        inputmethod0_.id as id1_3_0_,
        inputmethod0_.name as name4_3_0_,
        inputmethod0_.created_at as created_3_3_0_,
    from
        input_method inputmethod0_ 
    where
        inputmethod0_.id=?
```

#### logging.level.org.hibernate.type=trace
- 물음표로 표기된 bind parameter 값 출력
```
Hibernate: 
    select
        inputmethod0_.id as id1_3_0_,
        inputmethod0_.name as name4_3_0_,
        inputmethod0_.created_at as created_3_3_0_,
    from
        input_method inputmethod0_ 
    where
        inputmethod0_.id=?

TRACE 43178 --- [nio-8080-exec-2] o.h.type.descriptor.sql.BasicBinder      : binding parameter [1] as [BIGINT] - [2]
```
