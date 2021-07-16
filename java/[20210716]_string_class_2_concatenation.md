# String class 2 - String 연결
1. String 생성편 : [String class 1 - String 생성]([20210715]_string_class_1_creation.md)

---

# 👉 String 연결
- 네 가지 방법이 있다.

## 1. `+` 연산자
```java
String a = "a";
String b = "b";

String ab = a + b;
```
- 가장 쉽고 간편한 방법
- 이지만 컴퓨터의 입장에서는 추가 메모리가 필요하고 성능 저하를 일으킬 수도 있다.
- `"a" + "b"`이런 단순 연산에 사용하기 좋다.
- 다만 사이즈가 큰 Loop 돌릴 때는 한 번 생각해봄직하다.
  - 왜냐하면 String 클래스는 immutable, 즉 변경 불가능 클래스이기 때문.
  - 연산이 일어나면 값을 전부 복사해서 새로운 객체를 반환한다.
  - **n개의 문자열에 `+`연산자를 반복 적용해서 연결하는 데 드는 시간은, n^2에 비례한다.**

## 2. concat()
- SQL이나 JavaScript에서는 쓸 일이 종종 있었는데 자바에서는 한 번도 써본 적 없다.
```java
String str = "a".concat("b");
```
- 이렇게 쓴다고 한다.

## 3. StringBuffer, 4. StringBuilder
```java
StringBuffer stringBuffer = new StringBuffer();
stringBuffer.append("a");
stringBuffer.append("b");
```
```java
StringBuilder stringBuilder = new StringBuilder();
stringBuilder.append("a");
stringBuilder.append("b");
```
- 복사해서 새로운 객체를 반환하는 게 아니라 하나의 객체만을 가진다.
- String 자료형이 필요하면 `.toString()` 메서드 사용.
- **반복되는 연산을 할 때 만족스러운 성능을 얻으려면 String 대신 StringBuilder를 사용해야 한다.**

### StringBuffer vs StringBuilder
### StringBuffer 
  - 동기화 제공
  - 덕분에 StringBuilder 보다 느리다.
  - 멀티쓰레드 환경에서 동시에 객체에 접근하는 경우 사용
### StringBuilder
  - StringBuffer에서 동기화 기능을 뺀 것
  - 덕분에 StringBuffer 보다 빠르다.
  - 릴리즈 1.5에 추가
