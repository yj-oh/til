# useMemo, useCallback 제대로 사용하기(and 성능 최적화)
##### 📖 읽기 : https://kentcdodds.com/blog/usememo-and-usecallback

## 링크 요약
- 실행되는 모든 코드는 줄마다 비용이 든다.
- **최적화는 공짜가 아니다.**
    - 항상 들인 비용만큼 이득을 보진 않는다.
    - 최적화는 책임감 있게 해야 한다.
- **제품을 개선하는 데에 시간을 할애하는 게 더 이득.**
- 대부분의 경우 불필요한 리랜더링을 최적화 하지 않아도 된다.
    - 리액트는 매우 빠르다.
    - 최적화하는 것 말고도 할 것이 많다.
    - PayPal에서 3년 일하면서 필요한 상황 없었다.
- **it's best to measure first.**

### So when should I useMemo and useCallback?
- Referential equality
- Computationally expensive calculations
