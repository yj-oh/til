# Formatting numbers with comma
```java
import java.text.NumberFormat;

public class Main {
    /**
     * 숫자 천 단위 콤마 표시
     * @param num 포맷 변환할 숫자
     * @return String
     */
    public static String getFormatNumber(int num) {
    	return NumberFormat.getInstance().format(num);
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
    	System.out.println(getFormatNumber(100000));  // 100,000
    	System.out.println(getFormatNumber(1000000000));  // 1,000,000,000
    }
}
```
### NumberFormat.getInstance(Locale locale)
- 해당 Locale에 대한 형식 적용 
```java
public class Main {
    public static void main(String[] args) {
    	System.out.println("Locale.GERMANY : " + NumberFormat.getInstance(Locale.GERMANY).format(10000));
    	System.out.println("Locale.FRANCE  : " + NumberFormat.getInstance(Locale.FRANCE).format(10000));
    	System.out.println("Locale.KOREA   : " + NumberFormat.getInstance(Locale.KOREA).format(10000));
    }
}
```
```text
// 실행 결과
Locale.GERMANY : 10.000
Locale.FRANCE  : 10 000
Locale.KOREA   : 10,000
```
