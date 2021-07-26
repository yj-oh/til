# split() vs StringTokenizer
- 둘다 문자열을 분리하는 역할을 한다.

## split()
```java
package com.yjworld.java;

import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
    	String str = "앵,충,,춘식!춘복,,막렝,블루!!,,";

    	String[] strings = str.split("[,!]");

        System.out.println(strings.length);
    	System.out.println(Arrays.toString(strings));
    }
}
```
```text
8
[앵, 충, , 춘식, 춘복, , 막렝, 블루]
```
- 데이터가 없을 경우 공백을 반환한다.
- 여러개의 구분자를 사용하려면 `[,!]`와 같이 표현한다.
- 끝에 데이터가 없을 경우 무시한다.

## StringTokenizer
- 분해한 단위, 단위를 token이라고 한다.
```java
package com.yjworld.java;

import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) {
        String str = "앵,충,,춘식!춘복,,막렝,블루";

        StringTokenizer tokenizer = new StringTokenizer(str, ",!");

        System.out.println(tokenizer.countTokens());
        
        while (tokenizer.hasMoreTokens()) {
            System.out.println(tokenizer.nextToken());
        }
    }
}
```
```text
6
앵
충
춘식
춘복
막렝
블루
```
- `StringTokenizer`는 데이터가 없을 경우 무시한다. 그래서 count `6`
- 여러개의 구분자를 사용하려면 `,!`와 같이 줄줄 붙여 작성하면 된다.
- 끝에 데이터가 없을 경우 무시한다.

리턴타입 | 메소드 | 기능
--- | --- | ---
String | nextToken() | 파싱한 토큰 반환 (문자열 반환)
Object | nextElement() | 파싱한 토큰 반환 (객체 반환)
String | nextToken(String delim) | 새로운 구분자를 이용하여 파싱한 토큰 반환
boolean | hasMoreTokens() | nextToken 후 반환하지 않고 남아있는 토큰이 있는지 여부
boolean | hasMoreElements() | nextToken 후 반환하지 않고 남아있는 엘리먼트가 있는지 여부
int | countTokens() | 파싱한 토큰의 개수

## split() vs StringTokenizer

\- | split() | StringTokenizer
--- | --- | ---
차이점 | 메소드 | 클래스
중간에 데이터가 없을 경우 | 공백 반환 | 무시
끝에 데이터가 없을 경우 | 무시 | 무시
여러 개의 구분자를 사용하려면 | 정규표현식을 인자로 사용 <br/> e.g. [@#$%^&*] | 줄줄 쓰면 각각을 전부 구분자로 인식. <br/> e.g. "@#$%^&*"
