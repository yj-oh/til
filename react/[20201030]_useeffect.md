# useEffect

- Hook
- 컴포넌트가 마운트, 업데이트, 언마운트 될 때 동작

```jsx
import React, { useEffect } from 'react';

const Test = () => {
    useEffect(() => {
        console.log('mount');
        
        // cleanup 
        return () => {
            console.log('unmount');
        };
    }, []);
};
export default Test;
```

### deps
- 값을 넣어주면 값의 변경사항이 감지될 때마다 호출
- 생략하면 리렌더링 될 때마다 호출

```
⭐️️️️⭐️️️️⭐️️️️ (이거 몰랐을 때 엄청 삽질함.)

useEffect 안에서 사용하는 상태나, props 가 있다면, useEffect 의 deps 에 
넣어주어야 합니다. 그렇게 하는게, 규칙입니다.

만약 useEffect 안에서 사용하는 상태나 props 를 deps 에 넣지 않게 된다면 
useEffect 에 등록한 함수가 실행 될 때 최신 props / 상태를 가르키지 않게 됩니다.
```

##### * Reference : https://react.vlpt.us/basic/16-useEffect.html
