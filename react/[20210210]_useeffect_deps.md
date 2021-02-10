# useEffect deps에 조건 넣기
- useEffect의 deps가 무엇인지는 전에 정리했었다.
  - [useEffect]([20201030]_useeffect.md)
- 잘못 알고 있던 것이 있어서 정리.

## 코드
- status가 2일 때 실행하고 싶은 코드가 있을 때 아래와 같이 작성하면 된다고 생각했었다.
```jsx
useEffect(() => {
    // code...
}, [status === 2]);
```
- 하지만 제대로 동작하지 않아서 아래와 같은 코드로 고쳐쓴 적이 있다.
```jsx
useEffect(() => {
    if (status === 2) {
        // code...
    }
}, [status]);
```
- 무슨 차이?

## 설명
```jsx
useEffect(() => {
    // code...
}, [status === 2]);
```
- 위의 코드는 mount될 때 1회 실행된다.
- 그리고 status가 2일 때 `재실행`된다.

```jsx
useEffect(() => {
    if (status === 2) {
        // code...
    }
}, [status]);
```
- 위의 코드는 mount 때와 status가 업데이트될 때마다 실행되고
  status가 2일 때만 if문 내부의 코드를 실행한다.
