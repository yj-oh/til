# Convert date to milliseconds

### 상황
- 사용자가 **`2020-11-02`** 로 날짜를 지정해서 데이터를 저장
- UTC 기준의 DB에 **`2020-11-01 15:00:00`** 으로 저장
- 다시 조회해서 사용자에게 보여줄 때는 **`2020-11-02 00:00:00`**

### 문제
- 사용자가 **`2020-11-02`** 로 날짜를 지정해서 데이터를 저장
- UTC 기준의 DB에 **`2020-11-02 00:00:00`** 으로 저장
- 다시 조회해서 사용자에게 보여줄 때 **`2020-11-02 09:00:00`**로 나왔다.

### 기존
```javascript
export function convertToMilliseconds(date) {
    const d = new Date(date);
    return d.getTime();
}
```
```javascript
convertToMilliseconds("2020-11-02");
// const d = new Date(date);  // Mon Nov 02 2020 09:00:00 GMT+0900 (대한민국 표준시)
// d.getTime();               // 1604275200000
```

### 변경
```javascript
export function convertToMilliseconds(date) {
    const d = date ? new Date(date) : new Date();
    const userTimezoneOffset = d.getTimezoneOffset();
    return d.getTime() + (userTimezoneOffset * 60 * 1000);
}
```
```javascript
convertToMilliseconds("2020-11-02");
// const d = new Date(date);                        // Mon Nov 02 2020 09:00:00 GMT+0900 (대한민국 표준시)
// d.getTimezoneOffset();                           // -540
// d.getTime() + (userTimezoneOffset * 60 * 1000);  // 1604242800000
```

## getTimezoneOffset()
- 현재 타임존의 오프셋을 분 단위 숫자로 반환
- `-540`
   - 타임존이 UTC보다 540분 빠름.
   - 540 / 60 = 9시간 빠름.
