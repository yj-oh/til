# JUnit4 테스트 메소드 실행 순서 지정하기
- https://github.com/junit-team/junit4/wiki/test-execution-order

>- [@OrderWith (4.13 ~)](#@OrderWith)
>- [@FixMethodOrder (4.11 ~)](#@FixMethodOrder)

## @OrderWith
- 4.13 버전부터 가능
- Ordering 클래스에서 정의한 순서를 사용하여 테스트 메소드 실행
- https://junit.org/junit4/javadoc/latest/org/junit/runner/OrderWith.html

### 예제
#### [TestMethodOrder.java](https://github.com/junit-team/junit4/wiki/test-execution-order)
```java
import org.junit.Test;
import org.junit.runner.OrderWith;
import org.junit.runner.manipulation.Alphanumeric;

@OrderWith(Alphanumeric.class)
public class TestMethodOrder {

    @Test
    public void testA() {
        System.out.println("first");
    }
    @Test
    public void testB() {
        System.out.println("second");
    }
    @Test
    public void testC() {
        System.out.println("third");
    }
}
```
#### [Alphanumeric.java](https://github.com/junit-team/junit4/blob/main/src/main/java/org/junit/runner/manipulation/Alphanumeric.java)
```java
package org.junit.runner.manipulation;

import java.util.Comparator;

import org.junit.runner.Description;

/**
 * A sorter that orders tests alphanumerically by test name.
 *
 * @since 4.13
 */
public final class Alphanumeric extends Sorter implements Ordering.Factory {

    public Alphanumeric() {
        super(COMPARATOR);
    }

    public Ordering create(Context context) {
        return this;
    }

    private static final Comparator<Description> COMPARATOR = new Comparator<Description>() {
        public int compare(Description o1, Description o2) {
            return o1.getDisplayName().compareTo(o2.getDisplayName());
        }
    };
}
```

## @FixMethodOrder
- 4.11 버전부터 가능
- https://junit.org/junit4/javadoc/4.12/org/junit/FixMethodOrder.html

속성 | 설명
--- | ---
MethodSorters.DEFAULT | deterministic, 그러나 예측하기 힘들다.
MethodSorters.JVM | JVM에서 리턴되는 순서. 실행마다 다를 수 있다.
MethodSorters.NAME_ASCENDING | 메소드명 오름차순 

### 예제
```java
import org.junit.FixMethodOrder;
import org.junit.Test;
import org.junit.runners.MethodSorters;

@FixMethodOrder(MethodSorters.NAME_ASCENDING)
public class TestMethodOrder {

    @Test
    public void testA() {
        System.out.println("first");
    }
    @Test
    public void testB() {
        System.out.println("second");
    }
    @Test
    public void testC() {
        System.out.println("third");
    }
}
```
