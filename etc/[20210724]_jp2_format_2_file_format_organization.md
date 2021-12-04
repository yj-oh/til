# JP2 Format 2 - File Format Organization
1. Box 편 : [JP2 Format 1 - Box]([20210723]_jp2_format_1_box.md)
2. 👉 File Format Organization 편 : [JP2 Format 2 - File Format Organization]([20210724]_jp2_format_2_file_format_organization.md) 👈
- 참고 : [JPEG2000 Standard for Image Compression](https://books.google.co.kr/books?id=r8bi4kHC_bQC&pg=PA220&lpg=PA220&dq=jp2+box&source=bl&ots=KEEEb8aqLd&sig=ACfU3U0oMUCiahmElH7hdjUFwIwOS0YM5w&hl=en&sa=X&ved=2ahUKEwj5w4bS4fjxAhWNLqYKHWOJDaIQ6AEwC3oECAIQAw#v=onepage&q=jp2%20box&f=false)

---

- 필수로 구성되는 Box들이 있다.

![](.%5B20210724%5D_jp2_format_2_file_format_organization_images/24d4d2d5.png)

| Name                       | Type (TBox field in the box) |
|----------------------------|------------------------------|
| JP2 Signature box          | 'jP\032\032' (6A 50 1A 1A)h  |
| Profile box                | 'prfl' (70 72 66 6C)h        |
| JP2 Header box             | 'jp2h' (6A 70 32 68)h        |
| Image Header box           | 'ihdr' (69 68 64 72)h        |
| Color Specification box    | 'colr' (63 6F 6C 72)h        |
| Contiguous Code-Stream box | 'jp2c' (6A 70 32 63)h        |

## JP2 Signature box
- 무조건 첫번째로 오는 박스
- 12-byte string의 고정된 length를 가진다.
- value : 00 00 00 0C 6A 50 1A 1A 0D 0A 87 0A
  - 6A 50 20 20이 오는 애들도 있다. (뭔 차이지?)

## Profile box
- JP2 Signature box 바로 다음에 오는 박스
- TBox : 'prfl' (70 72 66 6C)h
- DBox : brand(BR), N 호환성 목록(CL)
- BR, CL은 ASCII 4-byte string으로 인코딩된다.
```text
profile box가 없을 경우 이 자리를 FileType Box (0x66747970)가 대신하는것 같다. 
File Type Box에서 LBox는 00 00 00 14로 20 byte 이며, 
TBox는 'ftyp' = (66 74 79 70)h 이고 
DBox는 6A 70 32 20 00 00 00 00 6A 70 32 20 이다.

(출처 : https://leemon.tistory.com/16 에서 가져옴.)
```

## JP2 Header box
- Image Header box와 하나 이상의 Color Specification box를 포함하는 superbox
- JP2 Signature box 뒤에, Contiguous Code-Stream box 앞에 와야 한다.
- TBox : 'jp2h' (6A 70 32 68)h

## Image Header box
- 24 바이트의 고정된 길이
- height, width, 컴포넌트 개수 등 이미지 정보를 가지고 있다.
- TBox : 'ihdr' (69 68 64 72)h
- DBox : 8개의 subfields

| Field Name | Description                | Size(bytes) | Value      |
|------------|----------------------------|-------------|------------|
| VERS       | Major/Minor version number | 2           | (01 00)h   |
| NC         | Number of components       | 2           | 1-(2^16-1) |
| HEIGHT     | Image height               | 4           | 1-(2^32-1) |
| WIDTH      | Image width                | 4           | 1-(2^32-1) |
| BPC        | Bits per component         | 1           | -127 ~ 127 |
| C          | Compression type           | 1           | 7          |
| UnkC       | Color space unknown        | 1           | 0 or 1     |
| IPR        | Intellectual property      | 1           | 0 or 1     |

## Color Specification box
- 압축 해제된 이미지 컴포넌트에 대한 색상 공간 지정
- TBox : 'colr' (63 6F 6C 72)h
- DBox : 5개의 subfields

| Field Name | Description               | Size(bytes)          | Value                                      |
|------------|---------------------------|----------------------|--------------------------------------------|
| METH       | Specification method      | 1                    | 1 = Enumerated, 2 = Restricted ICC Profile |
| PREC       | Precedence                | 1                    | 0                                          |
| APPROX     | Color space approximation | 1                    | 0                                          |
| EnumCs     | Enumerated color space    | 4(METH=1), 0(METH=2) | 0-(2^32-1) nonexistent                     |
| PROFILE    | ICC profile               | Varies               | Varies                                     |

## Contiguous Code-Stream box
- JPEG2000 code-stream
- LBox : 마지막 Box라서 0
- TBox : 'jp2c' (6A 70 32 63)h

## 샘플
- https://filesamples.com/formats/jp2 :sample1.jp2 파일 이용
- File to hex 변환

```text
// JP2 Signature box
00 00 00 0C 6A 50 20 20 0D 0A 87 0A

// Profile box가 없어서 FileType box
00 00 00 14  // LBox
66 74 79 70  // TBox
6A 70 32 20 00 00 00 00 6A 70 32 20  // DBox 

// JP2 Header box
00 00 00 2D  // LBox
6A 70 32 68  // TBox

// Image Header box
00 00 00 16 
69 68 64 72  // TBox
00 00 0E 75 00 00 0A 9D 00 03 07 07 01 00

// Color Specification box
00 00 00 0F  // LBox
63 6F 6C 72  // TBox
01 00 00 00 00 00 10 00 00 00 64 75 69 6E 66 
00 00 00 2A 75 6C 73 74 00 02 6A 70 6A 70 6A 
... 생략 ...
74 20 65 6E 64 3D 27 77 27 3F 3E 

// Contiguous Code-Stream box
00 00 00 00  // LBox
6A 70 32 63  // TBox

// JPEG marker - SOI (Start of image)
FF 4F ...
```
