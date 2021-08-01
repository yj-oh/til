# Streams vs collections
* 참고 : [stream 시작하기]([20210730]_getting_started_with_streams.md)

---

## 👉 1. 계산 시점
### 컬렉션
- 현재 자료구조가 포함하는 모든 값을 메모리에 저장
- 모든 요소는 컬렉션에 추가하기 전에 계산되어야 한다.
- e.g) 지하철역에서 아침에 파는 김밥 : 새벽에 김밥 100줄 미리 다 싸놓고 판매
### 스트림
- 요청할 때만 계산
- 게으르게 만들어지는 컬렉션
- e.g) 깁밥집에서 파는 김밥 : 주문이 들어오면 생산해서 판매

---
    
## 👉 2. 외부 반복과 내부 반복
### 컬렉션
- **외부 반복**
  - 명시적으로 컬렉션 항목을 하나씩 가져와서 처리
  - for-each 등을 사용해서 사용자가 직접 반복해야 한다.
  - 병렬성을 스스로 관리 (포기하든지, synchronized...)
### 스트림
- **내부 반복**
  - 데이터 표현과 하드웨어를 활용한 병렬성 구현을 자동으로 선택
  - 최적화된 처리 가능
    
![](.%5B20210801%5D_streams_vs_collections_images/2aecd198.png)
- *이미지 출처 : https://livebook.manning.com/book/java-8-in-action/chapter-4/*

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

public class Example {
    public static void main(String[] args) {

    List<Fruit> fruits = new ArrayList<>();
    fruits.add(new Fruit("apple", "green"));
    fruits.add(new Fruit("grape", "purple"));
    fruits.add(new Fruit("strawberry", "red"));

    // for-each 를 이용한 외부 반복
    List<String> fruitNames = new ArrayList<>();
    for (Fruit fruit : fruits) {
    	fruitNames.add(fruit.getName());
    }

    // 스트림 내부 반복
    List<String> fruitNames2 = fruits.stream()
            .map(Fruit::getName)
            .collect(Collectors.toList());

    }
}

class Fruit {
    private String name;
    private String color;

    public Fruit(String name, String color) {
    	this.name = name;
    	this.color = color;
    }

    public String getName() {
    	return name;
    }

    public String getColor() {
    	return color;
    }
}
```

##### Reference
- 책 ⌜모던 자바 인 액션⌟ 4장 스트림 소개 - 한빛미디어
