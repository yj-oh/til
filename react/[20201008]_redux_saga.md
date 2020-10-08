# redux-saga
- Redux로 side effects(데이터를 불러오는 비동기 처리나 브라우저 캐쉬에 접근하는 행위들)를 더 쉽게 다루기 위한 middleware
- 독립적인 실행 단위로써 각각 평행적으로 동작하는 "Task"의 개념을 Redux로 가져오기 위한 라이브러리
- generator, effect에 대한 이해 필요

### generator
- ES6 문법
- 참고 : [generator](../javascript/[20200930]_generator.md)

### effects
- `select` : State로부터 필요한 데이터를 꺼낸다.
- `put` : Action을 dispatch한다.
- `take` : Action을 기다린다. 이벤트의 발생을 기다린다.
- `call` : Promise의 완료를 기다린다.
- `fork` : 다른 Task를 시작한다.
- `join` : 다른 Task의 종료를 기다린다.
- 등등
- 💡 *Reference : https://github.com/reactkr/learn-react-in-korean/blob/master/translated/deal-with-async-process-by-redux-saga.md*
- 자세한 것은 https://redux-saga.js.org/docs/api/ 참고
