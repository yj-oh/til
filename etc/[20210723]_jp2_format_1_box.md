# JP2 Format 1 - Box
- 회사에서 일주일 내내 jp2랑 씨름을 했다.
- 그러면서 알게된 내용을 정리한다.
- 시리즈로 몇 편 나누어서 정리할 예정.
- 참고 : [JPEG2000 Standard for Image Compression](https://books.google.co.kr/books?id=r8bi4kHC_bQC&pg=PA220&lpg=PA220&dq=jp2+box&source=bl&ots=KEEEb8aqLd&sig=ACfU3U0oMUCiahmElH7hdjUFwIwOS0YM5w&hl=en&sa=X&ved=2ahUKEwj5w4bS4fjxAhWNLqYKHWOJDaIQ6AEwC3oECAIQAw#v=onepage&q=jp2%20box&f=false)

---

### JPEG2000 (JP2)
- image compression standard and coding system

## Box
- Fundamental building block
- JPEG2000의 code-stream, 기타 정보 등을 담고 있음.
- 4개의 field로 구성

![JP2 dox definition](.%5B20210723%5D_jp2_format_images/a5a91fed.png)

### LBox
- Length Box
- box의 length 명시
- 32-bit big-endian unsigned integer
- LBox 필드가 0인 box는 파일의 마지막 박스를 의미
- LBox 필드가 1인 box의 실제 length는 3번째 필드인 XLBox에 
  64-bit big-endian unsigned integer로 지정됨.

### TBox
- Type Box
- DBox에 저장되는 데이터의 타입 명시

### XLBox
- Extended Length Box
- box의 확장된 length 명시
- LBox가 1일 때 XLBox가 box의 실제 length가 된다.

### DBox
- Data Box
