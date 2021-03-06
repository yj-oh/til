# 📚 [Effective Java] 69. 예외는 진짜 예외 상황에만 사용하라

- 예외는 오직 예외 상황에서만 사용하고, 절대 일상적인 제어 흐름용으로 사용하지 않는다.
- 잘 설계된 API는 클라이언트가 정상적인 제어 흐름에서 예외를 사용할 일이 없어야 한다.
- '상태 의존적' 메서드를 제공하는 클래스는 '상태 검사' 메서드도 함께 제공하라.
  - ex) `Iterator` interface - `next`, `hasNext`

## 상태 검사 대신 아래와 같은 방법도 있다.
- 옵셔널, 특정값

### 1. 외부 동기화 없이 여러 스레드가 동시에 접근 가능하거나 외부 요인으로 상태가 변할 수 있을 때.
- 상태 검사 메서드와 상태 의존적 메서드 호출 사이에 객체의 상태가 변할 수 있으므로.

### 2. 성능이 중요한 상황에서 상태 검사 메서드가 상태 의존적 메서드의 작업 일부를 중복 수행할 때.

### 3. 다른 모든 경우에는 상태 검사 메서드 방식이 조금 더 낫다.
- 가독성이 살짝 더 좋다.
- 잘못 사용했을 때 발견하기 쉽다. (상태 의존적 메서드가 예외를 던져 버그를 확실히 드러냄.)
