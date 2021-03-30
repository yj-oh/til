# Date.prototype.getMonth() - zero-based value
- 작업하다가 충격적인 사실을 알게 되었다.

```javascript
console.log( new Date().getMonth() );
```

- 지금은 3월이지만 결과는 2다!

```text
The getMonth() method returns the month in the specified date according to local time, 
as a zero-based value (where zero indicates the first month of the year).
```
- _Reference : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getMonth_

- 근데 `getDate()`는 또 1부터다. 허, 참 신기하다. 왜 그랬을까.
- stackoverflow 고고
- https://stackoverflow.com/questions/2552483/why-does-the-month-argument-range-from-0-to-11-in-javascripts-date-constructor
  - 재밌는 답변이 많다.
