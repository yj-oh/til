# Object destructuring
- React를 하면서 특히 유용하게 사용 중.
```javascript
const book = {
    id: 1,
    title: 'Pro Git',
    created_at: '2021-03-23 00:00:00',
}

const { id, title, created_at } = book;

console.log(id);
console.log(title);
console.log(created_at);

// 1
// Pro Git
// 2021-03-23 00:00:00
```

## Default values
```javascript
const obj = {
    a: 1,
    c: 3,
}

const { a = 100, b = 200, c = 300 } = obj;

console.log(a);
console.log(b);
console.log(c);

// 1
// 202
// 3
```

## Assigning to new variable names
```javascript
const data = {
    created_at: '2021-03-28',
    updated_at: '2021-12-31',
}

const { created_at: createdAt, updated_at: updatedAt } = data;

console.log(createdAt);
console.log(updatedAt);
console.log(created_at);

// 2021-03-28
// 2021-12-31
// 🚨 Uncaught ReferenceError: created_at is not defined
```

##### * Reference : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#object_destructuring
