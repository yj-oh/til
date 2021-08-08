# indexOf(), lastIndexOf()
- 새삼스러운 정리...?!
- https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(int)

## indexOf()
- 지정된 문자를 `앞`에서부터 찾아서 첫 index 반환
- 찾는 문자가 없을 경우 -1 반환

```java
public int indexOf(String str) { }
public int indexOf(String str, int fromIndex) { }
```
```java
String str = "0123456789";

System.out.println( str.indexOf("5") );     // 5
System.out.println( str.indexOf("5", 4) );  // 5
System.out.println( str.indexOf("5", 6) );  // -1
```

## lastIndexOf()
- 지정된 문자를 `뒤`에서부터 찾아서 첫 index 반환
- 찾는 문자가 없을 경우 -1 반환
- ❗️ 뒤에서부터 찾는다고 해서 인덱스를 뒤에서부터 매기지는 않음. 앞에서부터 매긴 인덱스 반환.
- fromIndex 에서부터 앞으로 이동하며 찾는다.
```java
public int lastIndexOf(String str) { }
public int lastIndexOf(String str, int fromIndex) { }
```
```java
String str = "0123456789";

System.out.println( str.lastIndexOf("5") );     // 5
System.out.println( str.lastIndexOf("5", 4) );  // -1
System.out.println( str.lastIndexOf("5", 6) );  // 5
```
- str.lastIndexOf("5", 4)
  - 4부터 앞으로 이동하며 검색.
  - 4 - 3 - 2 - 1 - 0
  - "5"가 없으므로 -1
- str.lastIndexOf("5", 6)
    - 6부터 앞으로 이동하며 검색.
    - 6 - 5
