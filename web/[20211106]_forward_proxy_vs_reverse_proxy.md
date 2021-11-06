# Forward Proxy vs Reverse Proxy
- 여러 서버에 로드 분산, 웹 사이트 컨텐츠를 원활하게 표시, HTTP 이외의 프로토콜을 통해 처리 요청을 애플리케이션 서버에 전달

# 👉 Forward Proxy
- **⭐️ 클라이언트의 대리자**
- 클라이언트의 요청을 Proxy 서버가 받아 인터넷에 연결.
- 동일한 네트워크에 있는 여러 컴퓨터가 인터넷에 엑세스 하는 방법.
- 일반적으로 내부 네트워크에 존재.

![Forward Proxy](.%5b20211106%5d_forward_proxy_vs_reverse_proxy_images/ea036f93.png)

## 이점
- 내부 Cache 기능으로 성능 향상.
  - 만일 동일 네트워크의 다른 컴퓨터가 동일한 컨텐츠를 다운로드 하면 캐싱된 컨텐츠를 보내준다.
- 지리적으로 차단되거나 제한된 컨텐츠에 접근 가능.
- Original IP 주소를 숨길 수 있어 익명성 보장.
- 악의적 공격으로부터 `클라이언트` 보호.

# 👉 Reverse proxy
- **⭐️ 웹 서버의 대리자**
- 인터넷에서 요청을 받아 웹 서버에 전달.
- 주로 로드밸런싱, 고가용성을 위해 사용.
- 클라이언트가 웹 서버에 직접 엑세스하는 것을 제한.
  - 클라이언트는 프록시 서버하고만 통신, 프록시 서버는 웹 서버하고만 통신.
- 내부 서비스의 중앙 집중화, 인터넷에 대한 통합 인터페이스 제공
- Reverse proxy 기능을 제공하는 대표적인 서버 : `Nginx`, `Apache`

![Reverse Proxy](.%5b20211106%5d_forward_proxy_vs_reverse_proxy_images/9cdd33b0.png)

## 이점
- 로드 밸런싱
  - 서버 간 트래픽을 균등하게 분산
  - single point 장애 예방
- 보안
  - DDoS 공격 등 다양한 공격으로부터 `웹 서버` 보호
  - 정보를 숨기고 접근하는 요청 IP 를 차단하거나 연결 수 제한 가능
- 캐싱
- SSL termination
  - 웹 서버에 도달 전 요청을 복호화, 응답을 암호화 함으로써 웹 서버의 리소스 확보
- 확장성, 유연성
  - 클라이언트는 프록시의 IP 주소만 보기 때문에 웹 서버 인프라 구성을 자유롭게 변경 가능

# 👉 Forward Proxy vs Reverse Proxy
Topic | Forward Proxy | Reverse Proxy
--- | --- | ---
Proxy object | Client | Server
기능 | 클라이언트의 대리자 | 서버의 대리자
클라이언트 관점에서의 차이 | 클라이언트가 인터넷과 직접 통신하지 않도록 함 | 클라이언트가 서버와 직접 통신하지 않도록 함
클라이언트의 존재를 숨기는가 | ⭕️ | ❌
Origin 서버의 존재를 숨기는가 | ❌ | ⭕️

##### * References
- [Differences Between Forward Proxy and Reverse Proxy](https://www.linuxbabe.com/it-knowledge/differences-between-forward-proxy-and-reverse-proxy)
- [What is Reverse Proxy? Reverse Proxy Vs Forward Proxy](https://nlogn.in/what-is-reverse-proxy-reverse-proxy-vs-forward-proxy/)
- [stackoverflow - What's the difference between a proxy server and a reverse proxy server?](https://stackoverflow.com/questions/224664/whats-the-difference-between-a-proxy-server-and-a-reverse-proxy-server)
- [Nginx - What is a Reverse Proxy vs. Load Balancer?](https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/)
