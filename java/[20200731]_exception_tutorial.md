## 자바 예외 계층도
![java exception](.%5B20200731%5D_exception_images/java_exception.png)

## Error vs Exception
- `Error`
   - 코드로 수습될 수 없는 심각한 오류
   - 일단 발생하면 복구할 수 없다
- `Exception`
   - 코드로 수습될 수 있는 오류
   - 발생하더라도 개발자가 적절한 처리 코드를 작성함으로써 비정상적 프로그램 종료를 예방 가능
   
# Exception 

## Checked Exceptions vs Unchecked Exceptions
- `Checked Exceptions`
   - 확인된 예외
   - 메소드가 던질 수 있는 예외 목록을 선언하거나 try-catch로 처리
- `Unchecked Exceptions`
   - 프로그램을 실행하며 언제든 발생할 수 있는 예외
   - 메소드에 명시적으로 선언하지 않으면 호출자도 반드시 처리할 필요 없음
- ```text
  💡 대다수를 `Unchecked Exception`로 지정하고 꼭 필요한 상황에서만 `Checked Exception`로 지정
      → 불필요한 코드를 줄이기 위함
  ```

## Checked Exceptions
- `Exception` : 외적인 요인에 의해 발생 (사용자의 실수 등)

## RuntimeException (Unchecked)
- `RuntimeException` : 프로그래머의 실수에 의해 발생 
   - ArrayStoreException
   - BufferOverflowException
   - BufferUnderflowException
   - CannotRedoException
   - CannotUndoException
   - ClassCastException
   - CMMException
   - ConcurrentModificationException
   - DOMException
   - EmptyStackException
   - IllegalArgumentException
   - IllegalMonitorStateException
   - IllegalPathStateException
   - IllegalStateException
   - ImagingOpException
   - IndexOutOfBoundsException
   - MissingResourceException
   - NegativeArraySizeException
   - NoSuchElementException
   - NullPointerException
   - ProfileDataException
   - ProviderException
   - RasterFormatException
   - SecurityException
   - SystemException
   - UndeclaredThrowableException
   - UnmodifiableSetException
   - UnsupportedOperationException
