# HttpStatus Code 정리
*지속적으로 업데이트 중*

## 200
### Success
코드 | 의미 | 설명
--- | --- | ---
200 | Success | 요청 성공
201 | Created | 요청 성공, 새로운 resource 생성
203 | Non-Authoritative Information | 
204 | No Content | 요청 성공, 컨텐츠 없음

## 400
### Client Error
코드 | 의미 | 설명
--- | --- | ---
400 | Bad Request | The server could not understand the request due to invalid syntax. 요청이 유효하지 않아 더이상 작업을 진행하지 않음.
401 | Unauthorized | 인증 되지 않음
403 | Forbidden | 인증 되었으나 액세스 권한 없음
404 | Not Fount | The server can not find the requested resource
405 | Method Not Allowed | 요청이 허용되지 않는 메소드
409 | Conflict | 요청이 서버 상태와 충돌
415 | Unsupported Media Type | The media format of the requested data is not supported by the server, so the server is rejecting the request.

## 500
### Server Error
코드 | 의미 | 설명
--- | --- | ---
500 | Internal Server Error | 
502 | Bad Gateway |

##### * Reference : https://developer.mozilla.org/en-US/docs/Web/HTTP/Status
