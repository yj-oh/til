# styled-components
- `CSS-in-JS` : JavaScript 안에 스타일을 선언하는 방식
- 따로 스타일 시트를 만들지 않아도 컴포넌트.js에서 해결할 수 있는 점이 장점.

```
yarn add styled-components
```

### 예제
```javascript
import React from 'react';
import styled from 'styled-components';

const ViewBlock = styled.div`
  font-size:20px;
  text-align:center;
`;

const View = () => {
  return (
    <ViewBlock>
      <p>Hello, world!</p>
    </ViewBlock>
  );
};

export default View;
```

##### * Reference : ⌜리액트를 다루는 기술⌟ - 김민준 저 (⭐⭐⭐⭐⭐️강추)
