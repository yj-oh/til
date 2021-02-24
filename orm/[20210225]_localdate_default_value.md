# LocalDate default value
- LocalDate 타입에 기본값을 지정하고 싶었다.
- 다른 컬럼처럼 아래와 같이 Entity를 작성했다.
```java
@Column(nullable = false)
@ColumnDefault("9999-12-31")
private LocalDate endDate;
```

- 그리고 에러.
```text
You have an error in your SQL syntax; 
check the manual that corresponds to your MySQL server version 
for the right syntax to use near '-12-31 not null,
```

- 아래와 같이 수정했다.
```java
@Column(nullable = false, columnDefinition = "date default '9999-12-31'")
private LocalDate endDate;
```
