# 👉 HTTP
- Hypertext Transfer Protocol
- WWW 상에서 자원을 주고 받을 때 사용하는 통신 규약 프로토콜
  - 클라이언트(웹 브라우저)가 HTTP 통해 서버에 자원 요청, 서버가 이에 응답
- 80 포트
- 암호화 되지 않은 평문 데이터를 전송 → 보안 문제

# 👉 HTTPS
- Hypertext Transfer Protocol Secure
- HTTP의 확장
- SSL(Secure Socket Layer)을 사용하는 HTTP
- 433 포트
- 공개키 암호화, 개인키 암호화 방식

### 공개키, 개인키
- 공개키로 암호화 하면 개인키로만 복호화 가능
- 개인키로 암호화 하면 공개키로만 복호화 가능
- 공개키는 {공개키 저장소}에 등록, 개인키는 서버가 소유

### 공개키 저장소?
- CA(Certificate Authority)
- 전자서명을 이용한 전자상거래 등에서 객관적으로 신뢰할 수 있는 제3자(Trusted Third Party) 역할

# 👉 HTTPS 흐름
1. 개새낙이 HTTPS 적용을 위해 공개키, 개인키 생성
2. CA 기업과 계약
3. CA 기업 이름, 개새낙의 공개키, 공개키 암호화 방법, 서버 정보 등의 정보를 담은 인증서 생성
4. 해당 인증서를 CA 기업의 개인키로 암호화 해서 개새낙에게 제공 \
   → 개새낙은 `암호화된 인증서`를 획득했다!
5. 개새낙 서버에 암호화되지 않은 요청이 오면 `암호화된 인증서` 제공
6. **브라우저는 CA 기업의 공개키를 알고 있다.** \
   → 그 공개키로 `암호화된 인증서`를 복호화 \
   → 인증서에 담겨있던 개새낙의 공개키 정보 획득 \
   → 그렇게 획득한 개새낙 공개키로 데이터 암호화하여 요청 전송

# 💭 생각
```text
악의적인 클라이언트가 개새낙의 공개키를 획득했을 경우 
개새낙 서버에서 오는(개새낙의 개인키로 암호화된) 데이터를 복호화하여 볼 수 있지 않나?
보안이 철저하다고 할 수 있을까?
```
- 맞다. 그렇지만 해당 데이터가 이상한 곳에서 보낸 이상한 데이터가 아니라
  개새낙 서버가 인증한 데이터임을 보장할 수 있다.
  - 개새낙 공개키로 복호화해서 확인한 데이터라면 반드시 개새낙 개인키로 암호화된 데이터라는 것이고
  개새낙 개인키는 개새낙 서버만 가지고 있으므로
- 반대의 경우는 보안 철저하다.
  - 클라이언트가 개새낙에 보내는 데이터(개새낙 공개키로 암호화된 데이터)는
  개새낙 개인키로만 복호화 할 수 있으니 개새낙 서버 본인만 볼 수 있다.
