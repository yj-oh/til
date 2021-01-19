# react JavaScript 웹을 TypeScript로 바꿔보기
- 기존 JavaScript web : [react-news](https://github.com/yj-oh/react-news) 
```
yarn create-react-app ts-react-news --template typescript
```
- TypeScript web : [ts-react-news](https://github.com/yj-oh/ts-react-news)

---

## 👉 타입 정의
- `type` vs `interface`
  - `type` : 리터럴 타입의 값.
  - `interface` : Object. 상속이 일어날 수 있는 객체.
- `type` : 컴포넌트 이름 + Props
    ```typescript
    type NewsListProps = {
        // ...
    }
    
    function NewsList ({ category }: NewsListProps) { /* ... */ }
    ```
- `interface` : 앞에 `I` 붙일 필요 없음. 앞글자 대문자.

## 👉 확장자
- TypeScript file : `.ts`
- TypeScript JSX file : `.tsx`

## 👉 컴포넌트 구성
- 아직 지식이 깊지는 않지만 대충 이런 구조가 가장 코드 읽기 좋을 것이라고 생각.
```typescript jsx
// 1. import
import React from 'react';
import styled from 'styled-components';

// 2. styled-components
const StyledButton = styled.Button``;

// 3. 타입 선언
type NewsListProps = {
    title: string;
    content?: string;
}

// 4. 컴포넌트
function NewsList({ title, content }: NewsListProps) {
    // ...
}

// 5. 기본값 세팅
NewsList.defaultProps = {
    title: '기본 제목',
    content: '기본 내용',
}

export default NewsList;
```

## 👉 컴포넌트 작성
- arrow function이 아닌 일반 function () {}
    - 리액트 공식 문서나 해외의 유명 개발자들은 보통 function 키워드를 사용하여
      함수형 컴포넌트를 선언하는 것이 추세
      [(벨로퍼트와 함께하는 모던 리액트)](https://react.vlpt.us/using-typescript/02-ts-react-basic.html)
- `React.FC` 기본 타입 X
    - (아직까지는) defaultProps가 제대로 작동하지 않음.
    - props에 기본적으로 children이 들어가 있어서 옵셔널 불가.

---

##### * References
- [react + redux-saga + typescript 를 통한 프로젝트 구성과 컴포넌트 작성 가이드.](https://blog.woolta.com/categories/1/posts/197)
- [벨로퍼트와 함께하는 모던 리액트 - 8장. 리액트 프로젝트에서 타입스크립트 사용하기](https://react.vlpt.us/using-typescript/02-ts-react-basic.html)
