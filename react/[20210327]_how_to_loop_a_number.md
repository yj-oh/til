# JSX에서 숫자로 loop 돌기
```jsx
{Array.from(Array(5)).map((num, index) => (
    <p>{index}</p>
))}
```
```jsx
{[...Array(5)].map((num, index) => (
    <p>{index}</p>
))}
```

### 1부터
```jsx
{Array.from(Array(5)).map((num, index) => (
    <p>{++index}</p>
))}
```
```jsx
{[...Array(5)].map((num, index) => (
    <p>{++index}</p>
))}
```
