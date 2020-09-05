# Lifecycle

### Mount
- DOM이 생성되고 브라우저에 나타남

### Update
1. props 변경
2. state 변경
3. 부모 컴포넌트의 리렌더링
4. this.forceUpdate로 강제 렌더링 트리거

### Unmount
- 컴포넌트를 DOM에서 제거하고 브라우저에서 사라짐
