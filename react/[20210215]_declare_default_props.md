# Declare default props in functional component

## 방법1
```jsx
const Component = ({ props }) => {
    return <div>{props}</div>;
};
Component.defaultProps = {
    props: '기본값',
};
```

## 방법2
```jsx
const Component = ({ props = '기본값' }) => {
    return <div>{props}</div>;
};
```
```jsx
const Component = (props) => {
    const { id = 0, name = '기본값' } = props;

    return <div>{id} : {name}</div>;
};
```
