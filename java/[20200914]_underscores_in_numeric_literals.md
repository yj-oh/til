## 숫자 리터럴에 _(underscore)
- 가독성을 높이기 위해 숫자 리터럴 **사이**에 `underscore`를 사용할 수 있음
   - 숫자 천 단위로 comma 찍듯이

### ❌ 불가능한 케이스
- 숫자 시작 또는 끝
- 소수점 앞뒤
- 접미사 F, L, D 앞뒤

```java
int num = 1_000_000;    // ok
int num = _1_000_000;   // error : 숫자 앞
int num = 1_000_000_;   // error : 숫자 뒤

float f = 1_000_000F;   // ok
float f = 1_000_000F_;  // error : 접미사 F 뒤
float f = 1_000_000_F;  // error : 접미사 F 앞
float f = _1_000_000F;  // error : 숫자 앞

Double d = 1.000_111D;  // ok
Double d = 1_.000111D;  // error : 소수점 앞
Double d = 1._000111D;  // error : 소수점 뒤
Double d = 1.000111_D;  // error : 접미사 D 앞
Double d = 1.000111D_;  // error : 접미사 D 뒤
Double d = _1.000111D;  // error : 숫자 앞
```
