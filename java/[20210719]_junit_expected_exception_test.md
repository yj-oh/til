# JUnit Expected Exception Test
- 적절한 예외가 발생하는지 Test할 때는 `@Test`의 `expected`를 이용하면 편하다.
- JUnit 4에 추가된 기능이라고 함.

```java
@Test(expected = Exception.class)
public void test() {
    // ...
}
```

## 예제
```java
@Test(expected = ArrayIndexOutOfBoundsException.class)
public void test() {
    String[] fruits = { "apple", "banana", "grape" };

    for (int i = 0; i < 10; i++) {
        System.out.println( fruits[i] );
    }
}
```
- `ArrayIndexOutOfBoundsException`이 발생하면 테스트 통과.
- 예외가 발생하지 않거나, 다른 예외가 발생하면 테스트 실패.
