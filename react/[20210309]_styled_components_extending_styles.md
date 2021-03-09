# styled-components - extending styles
- `<Component />`라는 공통 컴포넌트가 있다.
- 내부에 styled-components 로 스타일을 적용해놓았다.
```jsx
const Test = () => {
    return <Component />;
}
```
- 공통 컴포넌트를 그대로 가져다 쓰는데, 특정 페이지에서만 스타일을 조금 다르게 주고 싶었다.
- 순간 `...?`
- 여태 잘 써왔으면서 새삼 띠용스러워서 정리한다.

## 상속
- styled-components 에는 상속의 개념이 있다.
- 특정 스타일을 상속하는 새 스타일을 만들기 위해서는 styled() constructor 를 사용하면 된다.

## 예제
```jsx
const Button = styled.button`
  border: solid 1px black;
`;

const RedButton = styled(Button)`
  background-color: red;
`;
```
- 그럼 `<RedButton/>`은 검은색 실선, 빨간색 배경의 버튼이 된다.
