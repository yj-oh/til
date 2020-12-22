# string to boolean

### `!!` 주의
- `!!'false'` → `true`

### `Boolean()` 주의
- `Boolean('false')` → `true`

```javascript
let string = 'true';

console.log( !!string );                // true
console.log( Boolean(string) );         // true
console.log( string === 'true' );       // true
console.log( string === 'false' );      // false
```
```javascript
let string = 'false';

console.log( !!string );                // ⚠️ true
console.log( Boolean(string) );         // ⚠️ true
console.log( string === 'true' );       // false
console.log( string === 'false' );      // true
```
```javascript
let string = 'TRUE';

console.log( !!string );                // true
console.log( Boolean(string) );         // true
console.log( string === 'true' );       // ⚠️ false
console.log( string === 'false' );      // ⚠️ false
```
```javascript
let string = 'FALSE';

console.log( !!string );                // ⚠️ true
console.log( Boolean(string) );         // ⚠️ true
console.log( string === 'true' );       // false
console.log( string === 'false' );      // false
```
