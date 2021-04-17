# console.table()
- Object를 어떻게 해야 콘솔에 깔끔하게 출력할 수 있을까?

## 예제 데이터
```javascript
const chunsik = { type: 'hamster', age: 1, like: 'yellow worm'};
const chung = { type: 'fish', age: 4, like: 'stone' };
const aeng = { type: 'fish', age: 4, like: 'food' };
```

## 보통 내가 쓰던 방법
```javascript
console.log(chunsik);
console.log(chung);
console.log(aeng);
```
```text
{type: "hamster", age: 1, like: "yellow worm"}
{type: "fish", age: 4, like: "stone"}
{type: "fish", age: 4, like: "food"}
```
![](.%5B20210417%5D_console_table_images/f58699c5.png)

## 위보다는 아래와 같이
```javascript
console.log({ chunsik, chung, aeng });
```
```text
{chunsik: {…}, chung: {…}, aeng: {…}}
  > aeng: {type: "fish", age: 4, like: "food"}
  > chung: {type: "fish", age: 4, like: "stone"}
  > chunsik: {type: "hamster", age: 1, like: "yellow worm"}
```
![](.%5B20210417%5D_console_table_images/21335844.png)

## console.table() 사용하기
- wow...
```javascript
console.table([ chunsik, chung, aeng ]);
```
![](.%5B20210417%5D_console_table_images/7fa74d43.png)

### 정렬
- 열을 클릭하면 정렬이 된다.

![](.%5B20210417%5D_console_table_images/1523260c.png)
  
### 원하는 컬럼만 출력
```javascript
console.table([ chunsik, chung, aeng ], ['age']);
```
![](.%5B20210417%5D_console_table_images/07f4e11d.png)

- 더 자세한 내용은 https://developer.mozilla.org/en-US/docs/Web/API/Console/table
