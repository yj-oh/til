 # Collections Framework?
 ```text
A collections framework is a unified architecture for representing and manipulating collections, 
enabling collections to be manipulated independently of implementation details.
```
- 컬렉션을 표현하고 다루기 위한 `통합 아키텍처`
   - *`컬렉션` : 여러 객체(데이터)를 모아놓은 것. 데이터 그룹.*
- 다수의 데이터를 쉽게 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합
- 데이터를 저장하는 자료구조와 데이터를 처리하는 알고리즘을 구조화하여 클래스로 구현해 놓은 것
- `인터페이스`와 `다형성`을 이용한 객체지향적 설계를 통해 표준화 되어있음

![https://www.javatpoint.com/collections-in-java](https://static.javatpoint.com/images/java-collection-hierarchy.png)
 
## 핵심 인터페이스 정리
| /    | 순서  | 중복                | 구현클래스                                     |
|------|-----|-------------------|-------------------------------------------|
| List | O   | O                 | ArrayList, LinkedList, Vector 등           |
| Set  | X   | X                 | HashSet, TreeSet 등                        |
| Map  | X   | key : X, value: O | HashMap, TreeMap, Hashtable, Properties 등 |

##### * Reference : [Java Documentation - Outline of the Collections Framework](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/reference.html)
