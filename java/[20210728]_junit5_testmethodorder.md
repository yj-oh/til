# JUnit5 테스트 메소드 실행 순서 지정하기 - @TestMethodOrder
- 클래스에 어노테이션으로 지정
- value
  - MethodOrderer.MethodName.class
  - MethodOrderer.DisplayName.class
  - MethodOrderer.OrderAnnotation.class
  - MethodOrderer.Random.class

## 👉 MethodName
```java
package com.yjworld.java;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.MethodOrderer;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.TestMethodOrder;

@TestMethodOrder(MethodOrderer.MethodName.class)
public class MainTest {

    @Test
    @DisplayName("1 : 메소드명 test3")
    void test3() { }

    @Test
    void test2() { }

    @Test
    @DisplayName("3 : 메소드명 test1")
    void test1() { }
}
```
#### 실행 순서
- void test1() { }
- void test2() { }
- void test3() { }

## 👉 DisplayName
```java
@TestMethodOrder(MethodOrderer.DisplayName.class)
public class MainTest {
    // 생략...
}
```
#### 실행 순서
- void test3() { }
- void test1() { }
- void test2() { }
* `DisplayName`이 지정된 애들이 우선 순위

## 👉 OrderAnnotation
```java
package com.yjworld.java;

import org.junit.jupiter.api.*;

@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
public class MainTest {

    @Test
    @DisplayName("1 : 메소드명 test3")
    @Order(1)
    void test3() { }

    @Test
    void test2() { }

    @Test
    @Order(3)
    @DisplayName("3 : 메소드명 test1")
    void test1() { }
}
```
#### 실행 순서
- void test3() { }
- void test1() { }
- void test2() { }
* `Order`가 지정된 애들이 우선 순위

## 👉 Random
```java
@TestMethodOrder(MethodOrderer.Random.class)
public class MainTest {
    // 생략...
}
```

## 👉 Custom
- MethodOrderer implements
```java
public class MethodOrdererImpl implements MethodOrderer {
    // Custom
}
```
- `@TestMethodOrder(MethodOrdererImpl.class)`와 같이 사용
