# Column mapping

| annotation  | description   |
|-------------|---------------|
| @Column     |               |
| @Enumerated | enum 타입       |
| @Temporal   | 날짜 타입         |
| @Lob        | BLOB, CLOB 타입 |
| @Transient  | mapping 하지 않음 |

## @Column
```java
@Column(
    name = "column_name", 
    nullable = true, 
    unique = false,
    columnDefinition = "comment 'comment'"
)
private String name;
```

## @Enumerated
```java
@Enumerated(EnumType.ORDINAL)
private InsulinType type;
```
- EnumType.ORDINAL `default`
   - 0, 1, 2 ...
   - 중간에 enum이 추가되거나 값이 변경되면 기존 데이터들의 값을 다 바꿔주어야 한다.
- EnumType.STRING

## @Temporal
- The type used in mapping java.util.Date or java.util.Calendar.
```java
@Temporal(TemporalType.TIMESTAMP)
private LocalDateTime createdAt;
```
- TemporalType.TIMESTAMP
- TemporalType.DATE
- TemporalType.TIME

## @Lob
```java
@Lob
private byte[] lobByte;
```

## @Transient
```java
@Transient
private String temp;
```
- DB 컬럼에 매핑하지 않고 임시로 값을 담고 싶을 때
