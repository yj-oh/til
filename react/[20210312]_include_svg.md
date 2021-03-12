# Include SVG

### In HTML
```html
<div>
    <object data="svg.svg" type="image/svg+xml"></object>
</div>
```

### In React
```jsx
import { ReactComponent as Svg } from '../assert/svg.svg';

const MyComponent = () => {
    return <Svg />;
}

export default MyComponent;
```
