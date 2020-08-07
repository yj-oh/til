# Package java.time
- JDK 1.8부터 추가
- 기존 Date, Calendar가 가지고 있던 단점을 해결
- 불변성 → 기존 객체를 변경하지 않고 항상 변경된, 새로운 객체 반환

## LocalDateTime
- 시간대(timezone)에 대한 정보가 없다.
- 한국에서의 `2020-08-07T00:00:00`가 미국에서도 `2020-08-07T00:00:00`
- 특정 이벤트 날짜 등에 적합
   - 생일 등
   
```java
import java.time.LocalDateTime;

public class Del1 { 
    public static void main(String[] args) { 
        System.out.println(LocalDateTime.now()); 
    }
}
// 출력 결과 : 2020-08-07T23:22:48.196359
```

- 객체 생성 시 of() 이용 - 다양한 형태의 of() 제공
    - of(int year, int month, int dayOfMonth, int hour, int minute)
    - of(int year, int month, int dayOfMonth, int hour, int minute, int second)
    - of(int year, int month, int dayOfMonth, int hour, int minute, int second, int nanoOfSecond)
    - of(int year, Month month, int dayOfMonth, int hour, int minute)
    - of(int year, Month month, int dayOfMonth, int hour, int minute, int second)
    - of(int year, Month month, int dayOfMonth, int hour, int minute, int second, int nanoOfSecond)
    - of(LocalDate date, LocalTime time)
    
## ZoneOffset
- UTC와의 차이
- 서울은 +9

```java
import java.time.ZonedDateTime;

public class Del1 { 
    public static void main(String[] args) { 
        System.out.println(ZonedDateTime.now().getOffset()); 
    }
}
// 출력 결과 : +09:00
```

## OffsetDateTime
- LocalDateTime + ZoneOffset

```java
import java.time.OffsetDateTime;

public class Del1 { 
    public static void main(String[] args) {
        System.out.println(OffsetDateTime.now()); 
    }
}
// 출력 결과 : 2020-08-07T23:52:12.826013+09:00
```

## ZonedDateTime
- OffsetDateTime + 지역

```java
import java.time.ZonedDateTime;

public class Del1 { 
    public static void main(String[] args) {
        System.out.println(ZonedDateTime.now()); 
    }
}
// 출력 결과 : 2020-08-07T23:46:55.633383+09:00[Asia/Seoul]
```

## Instant
- EPOCH TIME(1970-01-01 00:00:00 UTC)으로부터 경과된 시간을 나노초로 표기
- 단일 진법으로만 다루므로 계산하기 쉽다

```java
import java.time.Instant;

public class Del1 { 
    public static void main(String[] args) {
        System.out.println(Instant.now()); 
    }
}
// 출력 결과 : 2020-08-07T14:57:41.785659Z
```

##### * References
- ⌜JAVA의 정석⌟ - 남궁성 저 : Chapter 10 날짜와 시간
- https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html
