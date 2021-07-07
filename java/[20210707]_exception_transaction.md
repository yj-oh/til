# 예외 처리 - 트랜잭션
- 기본적인 예외와 에러에 대한 정보 : [Exception Tutorial]([20200731]_exception_tutorial.md)

---

## 🤔 상황
- pdf 파일을 jpeg 파일로 변환, 그 jpeg 파일을 dcm 파일로 변환한다.
- 뚝딱뚝딱 만들다가 정신을 차려보니 아래와 같은 구조가 나왔다.
```java
public class Converter {
    private void jpeg_변환() {
    	try {
            // pdf를 jpeg로 변환하여 output 디렉토리에 저장
        } catch(Exception e) {
            // output 디렉토리 삭제
        }
    }
    private void dcm_변환() {
        try {
            // jpeg를 pdf로 변환하여 output 디렉토리에 저장
            // jpeg 삭제
        } catch(Exception e) {
            // e.printStackTrace();
        }
    }
    public void convert() {
    	jpeg_변환();
    	dcm_변환();
    }
}
```

## 🤢 문제
### 🚨 jpeg_변환()에서 예외가 발생한 경우
- output 디렉토리가 삭제됨.
- dcm_변환()에서 FileNotFoundException 발생

### 🚨 dcm_변환()에서 2페이지 변환 중 예외가 발생한 경우
- output 디렉토리가 남아있음.
  - 1페이지 dcm 파일 생성됨.
  - 2페이지 jpeg 파일 남아있음.

### 이런 이상한 상황들이 생긴다.
- 실제 코드는 이보다 복잡하기 때문에 더 어메이징한 헬파티가 벌어질 수 있다.
- 어떤 과정에서든 예외가 발생한 경우에는 output 디렉토리를 깔끔하게 삭제하고
  변환을 **시작하기 전 상태로 돌아가야 한다.**
- 그래서 타이틀에 `트랜잭션`이라는 용어를 사용했다.
  - 단, 모든 상황이 이에 해당되지는 않는다.
  - **때로는 처음으로 돌아가지 않아야 할, 않아도 될 상황도 있을 수 있다.**
  - 이에 대한 판단은 개발자가 한다.
  
## 💡 해결
### 수정 전
```java
public class Converter {
    private void jpeg_변환() {
    	try {
            // pdf를 jpeg로 변환하여 output 디렉토리에 저장
        } catch(Exception e) {
            // output 디렉토리 삭제
        }
    }
    private void dcm_변환() {
        try {
            // jpeg를 pdf로 변환하여 output 디렉토리에 저장
            // jpeg 삭제
        } catch(Exception e) {
            // e.printStackTrace();
        }
    }
    public void convert() {
    	jpeg_변환();
    	dcm_변환();
    }
}
```
### 수정 후
```java
public class Converter {
    private void jpeg_변환() throws Exception {
        // pdf를 jpeg로 변환하여 output 디렉토리에 저장
    }
    private void dcm_변환() throws Exception {
        // jpeg를 pdf로 변환하여 output 디렉토리에 저장
        // jpeg 삭제
    }
    public void convert() {
    	try {
            jpeg_변환();
            dcm_변환();
        } catch (Exception e) {
    	    // output 디렉토리를 삭제한다.	
        }
    }
}
```
- 각각의 세부 단계에 해당하는 메소드는 예외를 처리하지 않고 단순히 바깥으로 던진다.
- convert 메소드에서 `try-catch`로 잡아 Exception 발생 시 디렉토리를 삭제한다.
  - **어떤 단계, 어느 메소드에서 예외가 발생하든 메소드 실행 전 초기 상태로 돌아갈 수 있다.**
