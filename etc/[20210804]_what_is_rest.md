# What is REST?
- Representational state transfer
- It is architectural style for distributed hypermedia systems.
  - 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처의 한 형식.

# REST의 6가지 기본 원칙

## 1. Client-server
```text
By separating the user interface concerns from the data storage concerns, 
we improve the portability of the user interface across multiple platforms 
and improve scalability by simplifying the server components.
```
- 사용자 인터페이스를 데이터 스토리지와 분리.
  - 여러 플랫폼에서의 이식성 향상.
  - 서버 컴포넌트를 단순화하여 확장성 향상.
    
## 2. Stateless
```text
Each request from client to server must contain all of the information 
necessary to understand the request, and cannot take advantage of 
any stored context on the server. Session state is therefore kept 
entirely on the client.
```
- 클라이언트에서 서버로의 request
  - 요청을 이해하기 위한 모든 정보를 포함해야 함.
  - 서버에 저장된 컨텍스트를 활용할 수 없음.
  - 고로 세션 상태는 전적으로 클라이언트에서 유지.
    
## 3. Cacheable
```text
Cache constraints require that the data within a response to a request 
be implicitly or explicitly labeled as cacheable or non-cacheable. 
If a response is cacheable, then a client cache is given the right to 
reuse that response data for later, equivalent requests.
```
- response에 캐시 가능 여부 명시.
- 캐시 가능하면 같은 요청이 왔을 때 response data 재사용할 수 있음.

## 4. Uniform interface
```text
By applying the software engineering principle of generality to the 
component interface, the overall system architecture is simplified 
and the visibility of interactions is improved. In order to obtain 
a uniform interface, multiple architectural constraints are needed to 
guide the behavior of components. REST is defined by four interface 
constraints: identification of resources; manipulation of resources 
through representations; self-descriptive messages; and, hypermedia 
as the engine of application state.
```
- 소프트웨어 엔지니어링 일반 원칙을 컴포넌트 인터페이스에 적용함으로써 
  전체 시스템 아키텍처의 단순함, 상호작용의 가시성 향상.
- 4가지 규약
  1. identification of resources
  2. manipulation of resources through representations
  3. self-descriptive messages
  4. hypermedia as the engine of application state
    
## 5. Layered system
```text
REST allows you to use a layered system architecture where you deploy 
the APIs on server A, and store data on server B and authenticate requests 
in Server C, for example. A client cannot ordinarily tell whether it is 
connected directly to the end server, or to an intermediary along the way.
```
- 계층화된 시스템 아키텍처 가능
- e.g) 서버 A에 API를 배치, 서버 B에 데이터를 저장, 서버 C에 요청 인증

## 6. Code on demand (optional)
```text
REST allows client functionality to be extended by downloading 
and executing code in the form of applets or scripts. This simplifies 
clients by reducing the number of features required to be pre-implemented.
```
- 애플릿이나 스크립트 형태로 다운로드, 실행해서 클라이언트 기능 확장 가능.
- 사전 구현에 필요한 기능의 수를 줄임으로써 클라이언트를 단순화함.

##### * Reference : https://restfulapi.net/
