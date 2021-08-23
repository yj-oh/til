# String class 1 - String 생성
1. 👉 String 생성편 : [String class 1 - String 생성]([20210715]_string_class_1_creation.md) 👈
2. String 연결편 : [String class 2 - String 연결]([20210716]_string_class_2_concatenation.md)
3. String 연결편 : [String class 3 - String 최적화]([20210717]_string_class_3_optimization.md)

---

- C 등 기존 다른 언어는 문자열을 char형의 배열로 다루었다.
- 자바는 클래스로 제공하는데, 그게 바로 String 클래스다.

---

# 👉 String 생성
- 문자열을 생성하면, String 객체는 `Heap 메모리의 어떤 공간`에 저장된다.

## String Pool
- 바로 그 Heap 메모리의 어떤 공간.
- == String Intern Pool or String Constant Pool

![String Pool Concept in Java](.%5B20210715%5D_string_class_images/0ad5139a.png)
https://static.javatpoint.com/core/images/string-pool-in-java.png

- String 리터럴을 생성하면 JVM이 `String pool`에서 같은 리터럴이 있는지 확인한다.
- 없으면 저장하고, 있으면 그 인스턴스의 참조를 반환한다.
- new 연산자로 생성한 애는 Heap의 `String pool`에 저장되는 게 아니라 그냥 `Heap`에 저장된다.

```java
String str  = "a";
String str2 = "a";

System.out.println( str.equals(str2) );  // true : 값이 같다
System.out.println( str == str2 );       // true : 참조하는 인스턴스가 같다
```
```java
String newStr  = new String("a");
String newStr2 = new String("a");

System.out.println( newStr.equals(newStr2) );  // true : 값은 같다
System.out.println( newStr == newStr2 );       // false : 참조하는 인스턴스가 다르다
```
```java
String str = "a";
String newStr = new String("a");

System.out.println( str.equals(newStr) );  // true : 값은 같다
System.out.println( str == newStr );       // false : 참조하는 인스턴스가 다르다
```
![](.%5B20210715%5D_string_class_images/54161439.png)
  
### String.intern()
```java
String internStr = new String("a").intern();
```
- new 연산자를 사용했지만 `Heap` 영역에 인스턴스를 새로 생성하는 것이 아니라 
  `String pool`에서 String.equals(Object) 메서드를 사용해서 같은 값이 있는지 찾는다.
- 없으면 `String pool`에 저장, 있으면 그 인스턴스의 참조를 반환한다.
- `String pool`의 사용을 강제하는 것이다.
- 그렇다면 아래 세 오브젝트를 각각 비교하면 결과가 어떨지 예상해보자.
```java
String str = "a";
String newStr = new String("a");
String internStr = new String("a").intern();
```
- str과 newStr은 값은 같고 참조하는 인스턴스는 다를 것이다.
- str과 internStr은 값도 같고 참조하는 인스턴스도 같을 것이다.
- newStr과 internStr은 값은 같고 참조하는 인스턴스는 다를 것이다.
```java
System.out.println( str.equals(newStr) );        // true
System.out.println( str == newStr );             // false
   
System.out.println( str.equals(internStr) );     // true
System.out.println( str == internStr );          // true

System.out.println( newStr.equals(internStr) );  // true
System.out.println( newStr == internStr );       // false
```
![](.%5B20210715%5D_string_class_images/6b05f7f4.png)

##### References
- 책 ⌜자바의 정석⌟ - 남궁성 지음, 도우출판
- https://www.javatpoint.com/string-pool-in-java
