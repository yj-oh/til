# styled-components - 공통 css 사용
- 공통된 CSS를 변수로 선언해서 재사용하기

## 예제
```jsx
import styled, { css } from 'styled-components';

const Fruit = css`
    width: 200px;
    height: 200px;
`;
const Apple = styled.div`
    ${css}
    background-color: red;
`;
const Banana = styled.div`
    ${css}
    background-color: yellow;
`;
```
