# \<option selected> 대신 \<select defaultValue>

## 상황
- 대략 이런 코드가 있었다.
```jsx
const { defaultValue } = props;

<select>
    {options && options.map((option) => (
        <option 
            key={option.id} 
            value={option.id}
            selected={option.id === defaultValue}
        >
            {option.name}
        </option>
    ))}
</select>
```

- 실행시키면 경고 뜬다.
```text
Warning: Use the 'defaultValue' or 'value' props on <select> 
instead of setting 'selected' on <option>
```

## 해결
```jsx
const { defaultValue } = props;

<select defaultValue={defaultValue}>
    {options && options.map((option) => (
        <option 
            key={option.id} 
            value={option.id}
        >
            {option.name}
        </option>
    ))}
</select>
```
