# Custom Hooks
- 반복되는 로직 재활용
- `use` 키워드로 시작
- 함수 작성
  - `useState`, `useEffect`, `useReducer`, `useCallback` 등 Hooks를 사용하여 원하는 기능 구현
  - 컴포넌트에서 사용하고 싶은 값 반환

##### * Reference : [벨로퍼트와 함께하는 모던 리액트 - 21. 커스텀 Hooks 만들기](https://react.vlpt.us/basic/21-custom-hook.html)

---

## 예제
- 사용자에게 경고, 에러 등의 메시지를 전달하기 위한 `MessageSlide`라는 컴포넌트를 만들었다.
- redux store의 message값이 바뀌면 slide가 출력되었다가 사라진다.
- 모든 페이지에서 이 에러 처리를 사용한다.
```jsx
import React, { useEffect } from 'react';
import { showMessage } from './MessageSlide';

const Page = () => {
    // ...
    
    useEffect(() => {
    	if (error) {
            dispatch(showMessage({ type: 'fail', message: error.message }));
            dispatch(initError());
    	}
    }, [error]);
    
    //...
}
export default Page;
```
- 그러다보니 똑같은 코드가 수십 번 반복된다.
- Custom Hooks를 사용해서 로직을 재사용해보도록 하자.

### src/hooks/useError.js 
- 디렉토리는 어디든 상관 없으니 적절한 곳에 생성하자.
```jsx
import { useEffect } from 'react';
import { useDispatch } from 'react-redux';
import { showMessage } from './MessageSlide';

export default function useError(error, initError) {
    const dispatch = useDispatch();
    useEffect(() => {
        if (error) {
            dispatch(showMessage({ type: 'fail', message: error.message }));
	        dispatch(initError);
        }
    }, [error]);
}
```
### 사용
```jsx
import React from 'react';
import useError from './hooks/useError';

const Page = () => {
    // ...
    
    // useEffect(() => {
    // 	if (error) {
    //         dispatch(showMessage({ type: 'fail', message: error.message }));
    //         dispatch(initError());
    // 	}
    // }, [error]);
    useError(error, initError());
    
    //...
}
export default Page;
```
- 이렇게 사용하는 게 맞나?
