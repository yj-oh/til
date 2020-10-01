# Middleware
- 액션을 디스패치 했을 때 리듀서에서 이를 처리하기에 앞서 사전에 지정된 작업들을 실행
- 액션과 리듀서 사이의 중간자
![](.%5B20201002%5D_middleware_images/ed4cd614.png)
- 함수를 반환하는 함수를 반환하는 함수
    ```javascript
    // 기본 구조
    const middleware = function middleware(store) {
        return function(next) {
            return function(action) {
                // ...
            } 
        }
    }
    ```
* *Referenct : ⌜리액트를 다루는 기술⌟ - 김민준 저*

## 왜 필요한가?
- 리덕스는 동기적으로 동작
   - 액션 객체 생성 → 디스패치가 스토어에 액션 발생을 알림 → 리듀서가 액션 처리 → 새로운 상태 반환
- 비동기적으로 처리해야 할 작업이 있다면 어떻게?
- 리덕스 미들웨어를 사용!

##### * 자세한 내용은 https://redux.js.org/advanced/middleware
