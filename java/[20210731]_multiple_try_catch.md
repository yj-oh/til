# 예외 처리 - 다중 catch
- try 문 내에 여러 개의 예외가 발생 가능할 경우, 다중 catch 문을 사용할 수 있다.
- 아래와 같은 형태.
- 위에서부터 순서대로 검사한다.
```java
try {
    // 로직
} catch (예외1) {
    // 예외1 발생 시 수행할 내용
} catch (예외2) {
    // 예외2 발생 시 수행할 내용
}
```

## 🚨 주의
- 하위 예외 클래스를 먼저 정의해야 한다.
- 상위 예외 클래스가 먼저 정의될 경우 아래의 예외는 절대 실행되지 않음.

### OK
```java
try {
    System.out.println(100 / 0);

} catch (ArithmeticException e) {
    System.out.println("ArithmeticException 발생!");

} catch (Exception e) {
    System.out.println("Exception 발생!");
}
```

### NOPE
```java
try {
    System.out.println(100 / 0);

} catch (Exception e) {
    System.out.println("Exception 발생!");
    
} catch (ArithmeticException e) {
    // 모든 예외의 상위 클래스는 Exception 클래스이므로 
    // 위에서 이미 다 잡히기 때문에 절대 실행되지 않는다.
    System.out.println("ArithmeticException 발생!");
}
```
- 위의 예제를 실행할 경우 아래와 같은 에러가 발생한다.
```text
java: exception java.lang.ArithmeticException has already been caught
```
