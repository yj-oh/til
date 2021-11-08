# nginx.conf 뜯어보기
- [Nginx 설치 후]([20211107]_install_nginx_on_ubuntu.md) `/etc/nginx/` 아래에 보면 자동으로 생성된 설정 파일이 있다.
- 하나 하나 살펴보자.
- 기본 파일 전문은 최하단에 기록해놓았다.

> 💡 _Notes_
> - _지시어별로 살펴본다._
> - _상단 예문은 공식 문서의 설명, 하단 예문은 실제 `nginx.conf`에 설정되어 있던 것이다._

---

- [Core module](#-core-module)
  - [user](#user)
  - [worker_processes](#worker_processes)
  - [pid](#pid)
  - [include](#include)
  - [events](#events)
  - [worker_connections](#worker_connections)
  - [multi_accept](#multi_accept)
  - [worker_connections](#worker_connections)
- [ngx_http_core_module](#-ngx_http_core_module)
  - [http](#http)
  - [sendfile](#sendfile)
  - [tcp_nopush](#tcp_nopush)
  - [tcp_nodelay](#tcp_nodelay)
  - [keepalive_timeout](#keepalive_timeout)
  - [types_hash_max_size](#types_hash_max_size)
  - [server_tokens](#server_tokens)
  - [server_names_hash_bucket_size](#server_names_hash_bucket_size)
  - [server_name_in_redirect](#server_name_in_redirect)
  - [types_hash_max_size](#types_hash_max_size)
  - [default_type](#default_type)
- [ngx_http_ssl_module](#-ngx_http_ssl_module)
  - [ssl_protocols](#ssl_protocols)
  - [ssl_prefer_server_ciphers](#ssl_prefer_server_ciphers)
- [ngx_http_log_module](#-ngx_http_log_module)
  - [access_log](#access_log)
  - [error_log](#error_log)
- [ngx_http_gzip_module](#-ngx_http_gzip_module)
  - [gzip](#gzip)
  - [gzip_vary](#gzip_vary)
  - [gzip_proxied](#gzip_proxied)
  - [gzip_comp_level](#gzip_comp_level)
  - [gzip_buffers](#gzip_buffers)
  - [gzip_http_version](#gzip_http_version)
  - [gzip_types](#gzip_types)
- [ngx_mail_core_module](#-ngx_mail_core_module)
- [nginx.conf : all](#-nginxconf--all)

---

# 👉 Core module
- http://nginx.org/en/docs/ngx_core_module.html
## user
```text
Syntax:  user user [group];
Default: user nobody nobody;
Context: main
```
```shell
user www-data;
```
- worker processes 에서 사용하는 사용자 자격 증명.
- 'root' 는 보안상 위험하므로 변경하는 것이 좋다.
> - ※ Ubuntu 에서 계정 추가, 삭제
> ```shell
> useradd {계정명}  # 추가. 계정만 생성, 홈 디렉토리와 패스워드는 따로 설정.
> ```
> ```shell
> deluser {계정명}  # 삭제
> ```

## worker_processes
```text
Syntax:  worker_processes number | auto;
Default: worker_processes 1;
Context: main
```
```shell
worker_processes auto;
```
- worker processes 의 개수
- 최적의 값은 CPU core 수, 하드디스크 드라이브 수, load pattern 등 여러 요인에 의해 결정됨.
- 확실하지 않을 대는 사용 가능한 CPU 코어 수로 설정하기.
- `auto`는 자동 감지.

> - ※ Ubuntu 에서 CPU core 수 확인하기
> ```shell
> nproc
> ```

## pid
```text
Syntax:  pid file;
Default: pid logs/nginx.pid;
Context: main
```
```shell
pid /run/nginx.pid;
```
- main process 의 process ID 를 저장할 파일

## include
```text
Syntax:  include file | mask;
Default: —
Context: any
```
```shell
include /etc/nginx/modules-enabled/*.conf;
```
- 다른 설정 파일을 include

## events
```text
Syntax:	events { ... }
Default:	—
Context:	main
```
- 비동기 이벤트 처리 방식에 대한 옵션 설정

## worker_connections
```text
Syntax:  worker_connections number;
Default: worker_connections 512;
Context: events
```
```shell
events {
    worker_connections 768;
}
```
- 하나의 worker process 가 열 수 있는 최대 커넥션 수

## multi_accept
```text
Syntax:  multi_accept on | off;
Default: multi_accept off;
Context: events
```
```shell
events {
    # multi_accept on;
}
```
- on : worker process 가 `한 번에 모든` 새 커넥션 수락.
- off : worker process 가 `한 번에 하나`의 새 커넥션 수락.

---

# 👉 ngx_http_core_module
- https://nginx.org/en/docs/http/ngx_http_core_module.html

## http
```text
Syntax:	 http { ... }
Default: —
Context: main
```
- HTTP server 지시문을 사용한 환경 파일 컨텍스트

## sendfile
```text
Syntax:  sendfile on | off;
Default: sendfile off;
Context: http, server, location, if in location
```
```shell
http {
    sendfile on;
}
```
- 설명을 읽어보았지만 무슨 말인지 모르겠음.

## tcp_nopush
```text
Syntax:	 tcp_nopush on | off;
Default: tcp_nopush off;
Context: http, server, location
```
```shell
http {
    tcp_nopush on;
}
```
- FreeBSD 에서의 TCP_NOPUSH 소켓 옵션, Linux 에서의 TCP_CORK 소켓 옵션
- [`sendfile`](#sendfile)을 사용할 때에만 활성화 된다.

## tcp_nodelay
```text
Syntax:	 tcp_nodelay on | off;
Default: tcp_nodelay on;
Context: http, server, location
```
```shell
http {
    tcp_nodelay on;
}
```
- connection 이 keep-alive 로 전환될 때 활성화 된다.

> - [Keep-Alive](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Keep-Alive)

## keepalive_timeout
```text
Syntax:	 keepalive_timeout timeout [header_timeout];
Default: keepalive_timeout 75s;
Context: http, server, location
```
```shell
http {
    keepalive_timeout 65;
}
```
- keep-alive timeout 시간
- 0 이면 keep-alive 비활성화.

## types_hash_max_size
```text
Syntax:	 types_hash_max_size size;
Default: types_hash_max_size 1024;
Context: http, server, location
```
```shell
http {
    types_hash_max_size 2048;
}
```
- [hash tables](https://nginx.org/en/docs/hash.html) 의 최대 사이즈

## server_tokens
```text
Syntax:	 server_tokens on | off | build | string;
Default: server_tokens on;
Context: http, server, location
```
```shell
http {
    # server_tokens off;
}
```
- 에러 페이지와 서버 response header 필드에 Nginx 버전 표기 여부
- 보안상 `on` 설정을 하는 것이 좋다고 함.

## server_names_hash_bucket_size
```text
Syntax:	 server_names_hash_bucket_size size;
Default: server_names_hash_bucket_size 32|64|128;
Context: http
```
```shell
http {
    # server_names_hash_bucket_size 64;
}
```
- server_names_hash 에 대한 bucket 사이즈 설정
- 설정된 사이즈보다 긴 도메인을 사용할 경우 에러가 발생할 수 있다.

## server_name_in_redirect
```text
Syntax:  server_name_in_redirect on | off;
Default: server_name_in_redirect off;
Context: http, server, location
```
```shell
http {
    # server_name_in_redirect off;
}
```
- absolute 리디렉션에서 server_name 에 지정한 이름을 사용할 것인지 여부

## include(dup)
```shell
http {
    include /etc/nginx/mime.types;
}
```
- core module 의 include 설명 참고

## default_type
```text
Syntax:	 default_type mime-type;
Default: default_type text/plain;
Context: http, server, location
```
```shell
http {
    default_type application/octet-stream;
}
```
- response 의 기본 MIME 유형

---

# 👉 ngx_http_ssl_module
- https://nginx.org/en/docs/http/ngx_http_ssl_module.html

## ssl_protocols
```text
Syntax:	 ssl_protocols [SSLv2] [SSLv3] [TLSv1] [TLSv1.1] [TLSv1.2] [TLSv1.3];
Default: ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
Context: http, server
```
```shell
http {
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
}
```
- 지정된 프로토콜 활성화
```text
The TLSv1.1 and TLSv1.2 parameters (1.1.13, 1.0.12) work only 
when OpenSSL 1.0.1 or higher is used.

The TLSv1.3 parameter (1.13.0) works only 
when OpenSSL 1.1.1 or higher is used.
```

## ssl_prefer_server_ciphers
```text
Syntax:	 ssl_prefer_server_ciphers on | off;
Default: ssl_prefer_server_ciphers off;
Context: http, server
```
```shell
http {
    ssl_prefer_server_ciphers on;
}
```
- on 설정 시 SSLv3, TLS 프로토콜 사용할 때 클라이언트 암호보다 서버 암호의 우선 순위가 높다.

---

# 👉 ngx_http_log_module
- https://nginx.org/en/docs/http/ngx_http_log_module.html
- https://docs.nginx.com/nginx/admin-guide/monitoring/logging/

## access_log
```text
Syntax:	 access_log path [format [buffer=size] [gzip[=level]] [flush=time] [if=condition]];
         access_log off;
Default: access_log logs/access.log combined;
Context: http, server, location, if in location, limit_except
```
```shell
http {
    access_log /var/log/nginx/access.log;
}
```

>#### 사용 예제
> ```shell
> log_format combined '$remote_addr - $remote_user [$time_local] '
>                     '"$request" $status $body_bytes_sent '
>                     '"$http_referer" "$http_user_agent"';
> ```
> - 로그 포맷을 위와 같이 `combined`라는 이름으로 설정하고,
> ```shell
> access_log /var/log/nginx/access.log combined;
> ```
> - 위와 같이 access_log 설정을 하면 해당 경로에 지정한 포맷에 맞게 로그를 생성한다.
> - 예시를 위한 것이다. format 을 설정하지 않으면 "combined"으로 기본 설정된다고 함.

## error_log
```text
Syntax:	 error_log file [level];
Default: error_log logs/error.log error;
Context: main, http, mail, stream, server, location
```
```shell
http {
    error_log /var/log/nginx/error.log;
}
```
- 에러 로깅
- Level : debug, info, notice, warn, error, crit, alert, or emerg (낮음 → 높음 순서)
    - `debug` : 디버깅
    - `info` : 정보
    - `notice` : 주목할 만한 가치가 있는 정상적인 일
    - `warn` : 경고
    - `error` : 처리 실패
    - `crit` : 프로세스에 크리티컬한 문제 발생
    - `alert` : 신속한 조치 필요
    - `emerg` : 서비스 불가 수준의 긴급한 에러
- context 를 보면 알 수 있듯이 전역적으로 설정할 수도 있고 서버 별로 설정할 수도 있다.

---

# 👉 ngx_http_gzip_module
- https://nginx.org/en/docs/http/ngx_http_gzip_module.html

## gzip
```text
Syntax:	 gzip on | off;
Default: gzip off;
Context: http, server, location, if in location
```
```shell
http {
    gzip on;
}
```
- response 압축 여부

## gzip_vary
```text
Syntax:	 gzip_vary on | off;
Default: gzip_vary off;
Context: http, server, location
```
```shell
http {
    # gzip_vary on;
}
```
- gzip 이 활성화된 경우 response 헤더 필드 - "Vary: Accept-Encoding" 삽입 여부

## gzip_proxied
```text
Syntax:	 gzip_proxied off | expired | no-cache | no-store | private | no_last_modified | no_etag | auth | any ...;
Default: gzip_proxied off;
Context: http, server, location
```
```shell
http {
    # gzip_proxied any;
}
```
- 프록시나 캐시 서버에서 요청할 경우의 동작 여부
- 프록시 여부는 via 헤더의 존재 여부로 확인한다.
- multiple parameters 허용
    - `off` : 항상 압축 비활성화
    - `expired` : "Expires" 필드가 있고 만료되었을 때 압축
    - `no-cache` : "Cache-Control" 필드가 있고 "no-cache"일 때 압축
    - `no-store` : "Cache-Control" 필드가 있고 "no-store"일 때 압축
    - `private` : "Cache-Control" 필드가 있고 "private"일 때 압축
    - `no_last_modified` : "Last-Modified" 필드가 없으면 압축
    - `no_etag` : "ETag" 필드가 없으면 압축
    - `auth` : "Authorization" 필드가 있으면 압축
    - `any` : 항상 압축 활성화

## gzip_comp_level
```text
Syntax:	 gzip_comp_level level;
Default: gzip_comp_level 1;
Context: http, server, location
```
```shell
http {
    # gzip_comp_level 6;
}
```
- response 압축 레벨
- 1 ~ 9 : 숫자가 클수록 압축율은 올라가지만 속도는 느려짐

## gzip_buffers
```text
Syntax:	 gzip_buffers number size;
Default: gzip_buffers 32 4k|16 8k;
Context: http, server, location
```
```shell
http {
    # gzip_buffers 16 8k;
}
```
- response 를 압축하는 데 사용되는 버퍼의 개수와 크기

## gzip_http_version
```text
Syntax:	 gzip_http_version 1.0 | 1.1;
Default: gzip_http_version 1.1;
Context: http, server, location
```
```shell
http {
    # gzip_http_version 1.1;
}
```
- 압축에 필요한, request 의 최소 HTTP 버전

## gzip_types
```text
Syntax:	 gzip_types mime-type ...;
Default: gzip_types text/html;
Context: http, server, location
```
```shell
http {
    # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
}
```
- 압축할 MIME types

---

# 👉 ngx_mail_core_module
- https://nginx.org/en/docs/mail/ngx_mail_core_module.html
- 생략한다. 위 링크 참고.

---

# 📂 nginx.conf : all

```shell
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
	worker_connections 768;
	# multi_accept on;
}

http {

	##
	# Basic Settings
	##

	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;
	# server_tokens off;

	# server_names_hash_bucket_size 64;
	# server_name_in_redirect off;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	##
	# SSL Settings
	##

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
	ssl_prefer_server_ciphers on;

	##
	# Logging Settings
	##

	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;

	##
	# Gzip Settings
	##

	gzip on;

	# gzip_vary on;
	# gzip_proxied any;
	# gzip_comp_level 6;
	# gzip_buffers 16 8k;
	# gzip_http_version 1.1;
	# gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

	##
	# Virtual Host Configs
	##

	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}


#mail {
#	# See sample authentication script at:
#	# http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
#
#	# auth_http localhost/auth.php;
#	# pop3_capabilities "TOP" "USER";
#	# imap_capabilities "IMAP4rev1" "UIDPLUS";
#
#	server {
#		listen     localhost:110;
#		protocol   pop3;
#		proxy      on;
#	}
#
#	server {
#		listen     localhost:143;
#		protocol   imap;
#		proxy      on;
#	}
#}
```
