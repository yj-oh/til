# 구분자 포함하여 문자열 이어붙이기 - StringJoiner

## 🤔 StringBuilder 사용
- 과일 쇼핑을 하자.
```java
package com.yjworld.java;

import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
    	// 지금은 여름
    	final String season = "summer";
    	
    	// 쇼핑 카트에 과일을 담자
    	StringBuilder shoppingCart = new StringBuilder();
        shoppingCart.append("사과 ");
        shoppingCart.append("딸기 ");
        shoppingCart.append("포도 ");

        // 여름이면 자두도 담자
    	if ("summer".equals(season)) {
            shoppingCart.append("자두");
    	}

    	// 마지막에는 꼭 파인애플을 산다
        shoppingCart.append("파인애플");
    	
    	String fruits = shoppingCart.toString();
    	
    	// 과일 상자에 담자 
    	String[] fruitsBox = fruits.split(" ");

    	// 뭐가 담겼는지 확인하자
    	System.out.println(Arrays.toString(fruitsBox));
    }
}
```
```text
[사과, 딸기, 포도, 자두파인애플]
```
- `shoppingCart.append("자두")` 때문에 존재하지도 않는 `자두파인애플`이 담겼다.
- 구분자로 공백 문자를 사용하는데 자두는 그걸 빼먹었기 때문이다.
- 이런 일이 생긴다.
```java
shoppingCart.append("사과");
shoppingCart.append(" ");
shoppingCart.append("딸기");
shoppingCart.append(" ");
shoppingCart.append("포도");
shoppingCart.append(" ");
// ...
```
- 이런 방법도 있지만 저것도 빼먹으면 그만이고 지저분하고 별로다.

## 🤓 StringJoiner 사용
- `StringJoiner`라는 아이가 있다.
- `StringBuilder`를 `StringJoiner`로, append()를 add()로 바꾸자.
```java
package com.yjworld.java;

import java.util.Arrays;
import java.util.StringJoiner;

public class Main {
    public static void main(String[] args) {
        final String season = "summer";

        // 생성자에 구분자를 넣어주자.
        StringJoiner shoppingCart = new StringJoiner(" ");
        shoppingCart.add("사과");
        shoppingCart.add("딸기");
        shoppingCart.add("포도");

        if ("summer".equals(season)) {
            shoppingCart.add("자두");
        }

        shoppingCart.add("파인애플");

        String fruits = shoppingCart.toString();
        String[] fruitsBox = fruits.split(" ");

        System.out.println(Arrays.toString(fruitsBox));
    }
}
```
```text
[사과, 딸기, 포도, 자두, 파인애플]
```
- 개발자가 신경쓸 것 없이 알아서 구분자 넣어 문자열 이어붙여준다.

* https://docs.oracle.com/javase/8/docs/api/java/util/StringJoiner.html
* https://www.javatpoint.com/java-stringjoiner
