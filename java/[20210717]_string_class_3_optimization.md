# String class 3 - String 최적화
1. String 생성편 : [String class 1 - String 생성]([20210715]_string_class_1_creation.md)
2. String 연결편 : [String class 2 - String 연결]([20210716]_string_class_2_concatenation.md)

---

# 👉 String 최적화
- `+` 연산자
- concat()
- StringBuffer
- StringBuilder

## `+` 연산자
```java
int num = 10000;

String output = "";

long before = System.currentTimeMillis();

for (int i = 0; i < num; i++) {
    output += "a";
}
long after = System.currentTimeMillis();
System.out.println(after - before);
```
- 이후 코드에서는 시간 측정/계산 코드를 생략한다.

## concat()
```java
int num = 10000;

String output = "";

for (int i = 0; i < num; i++) {
    output = output.concat("a");
}
```

## StringBuffer
```java
int num = 10000;

StringBuffer output = new StringBuffer();

for (int i = 0; i < num; i++) {
    output.append("a");
}
```

## StringBuilder
```java
int num = 10000;

StringBuilder output = new StringBuilder();

for (int i = 0; i < num; i++) {
    output.append("a");
}
```

## 비교
Loop | + | concat() | StringBuffer | StringBuilder
--- | --- | --- | --- | ---
100 | 15 | 0 | 0 | 0
1000 | 18 | 0 | 1 | 0
10000 | 39 | 17 | 2 | 1
100000 | 767 | 736 | 7 | 6
1000000 | 43922 | 56982 | 20 | 18

- `+` 연산자와 `StringBuilder`의 성능은 연산 횟수가 늘어날수록 엄청난 차이를 보인다.

## 👍 결론
- 문자열 연결 시에는 성능을 신경쓸 것.
- 간단한 연산에는 `+` 연산자가 간편할 수 있다.
- 성능이 걱정될 때는 `+` 연산자 대신 `StringBuilder.append()` 사용할 것.

##### Reference
- 책 ⌜이펙티브 자바 2판⌟ 규칙 51. 문자열 연결 시 성능에 주의하라 - 조슈아 블로크 지음, 인사이트
