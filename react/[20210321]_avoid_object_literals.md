# Object literals 피하기
- Object literals don’t have a persistent memory space
  - 컴포넌트가 리렌더링 될 때마다 새로 메모리 할당
- 성능에 영향을 줄 수 있다.

## 예제
```jsx
import React from 'react';
import SubComponent from './SubComponent';

const MainComponent = () => {
    return <SubComponent style={{ backgroundColor: 'red' }} />;
};

export default MainComponent;
```
- `<MainComponent />`가 렌더링될 때마다 새로운 Object literal이 메모리에 생성됨.
- `memo`, `PureComponent`도 이를 막을 수 없다.

## 해결
```jsx
const style = { backgroundColor: 'red' };

const MainComponent = () => {
    return <SubComponent style={style} />;
};
```

##### * References
- https://www.digitalocean.com/community/tutorials/react-keep-react-fast
- https://marmelab.com/blog/2017/02/06/react-is-slow-react-is-fast.html#beware-of-object-literals-in-jsx
