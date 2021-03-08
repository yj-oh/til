# Named export vs Default export (ES6)

## Named export
- 한 파일 당 여러 개의 export 가능
```jsx
export const StyledButton = () => {}
export const StyledTable = () => {}
```

- exported module, import module 이름 동일해야 함.
```jsx
import { StyledButton, StyledTable } from './ThemeComponent';
```

- 대신 Alias 줄 수 있음.
```jsx
import { StyledButton as Button } from './ThemeComponent';
```

- 전체 import
```jsx
import * as ThemeComponent from './ThemeComponent';

// use
ThemeComponent.StyledButton
ThemeComponent.StyledTable
```

## Default export
- 한 파일 당 하나의 export
- exported module, import module 이름 달라도 됨.
```jsx
import { DefaultThemeComponent } from './ThemeComponent';
```
