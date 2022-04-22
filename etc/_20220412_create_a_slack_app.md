# 슬랙 앱 만들기

# 👉 1. 봇 생성
- https://api.slack.com/

![](._20220412_create_a_slack_app_images/d7eb2391.png)

![](._20220412_create_a_slack_app_images/c15e8093.png)

- App Name 입력, workspace 선택

![](._20220412_create_a_slack_app_images/51058a31.png)

![](._20220412_create_a_slack_app_images/9a442f29.png)

![](._20220412_create_a_slack_app_images/6301f3a6.png)

- OAuth & Permissions 페이지 밑에 내려보면 `Scopes`이 있다. 
- Bot token Scopes 눌러서 필요한 권한을 선택해준다.

![](._20220412_create_a_slack_app_images/4d8c3fe0.png)

| OAuth Scope   | Description        |
|---------------|--------------------|
| channels:read | public 채널 정보 조회 권한 |
| chat:write    | 메시지 발송 권한          |

![](._20220412_create_a_slack_app_images/82e5d41a.png)

- Access 페이지 나오면 allow 눌러준다.
- 그럼 token 이 생성되는데, 필요하니 복사해두자.

![](._20220412_create_a_slack_app_images/1a4cc9dc.png)

# 👉 채널 생성 및 앱 연결, 채널 정보 얻기
- 채널 생성은 생략. 
- ###⭐️ 단, 반드시 공개 채널로 생성할 것!

![](._20220412_create_a_slack_app_images/1d374ae0.png)

- 채널 이름 클릭하면 모달 하나 뜨는데, 통합 탭에서 앱 추가를 해준다.
- 그리고 위에서 만들어준 봇을 연결한다.

- 테스트 해본다
- https://api.slack.com/methods/conversations.list/test

![](._20220412_create_a_slack_app_images/859b1e1a.png)

- 아까 복사해둔 token 넣고 `Test method` 버튼 클릭
- 그럼 json 형태로 채널 목록 응답값이 오는데, 봇 연결한 채널 찾아서 id 값을 알아둔다.

# 👉 Chat API 테스트
- https://api.slack.com/methods/chat.postMessage/test

![](._20220412_create_a_slack_app_images/4fa8b030.png)

- 토큰과 채널 id, text 를 넣고 테스트 돌려서 슬랙에 메시지가 오는지 확인한다.

# 👉 코드 작성
- https://api.slack.com/messaging/sending
- 이 문서를 참고 했다.
