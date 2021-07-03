# GitHub personal access token 사용하기 (403 권한 없음 오류)

## 🤔 상황
- 7월 1일 2AM경...
- 룰루랄라 즐거운 코딩을 끝내고 GitHub에 작업한 코드 Push 하려는데 403 오류가 떴다.

```text
remote: Password authentication is temporarily disabled as part of 
a brownout. Please use a personal access token instead.
remote: Please see https://github.blog/2020-07-30-token-authentication-requirements-for-api-and-git-operations/ for more information.
fatal: unable to access 'https://github.com/yj-oh/til.git/':
The requested URL returned error : 403
```

- 으아니, 분명 잘 되던 게 설정을 건들인 것도 아닌데 갑자기?
- 하고 메시지를 잘 보니.

```text
Password authentication is temporarily disabled as part of 
a brownout. Please use a personal access token instead.
```

- 알고보니 예고가 되어있었다.
  - [The GitHub Blog - Token authentication requirements for Git operations (2020-12-15)](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)
>#### June 30, 2021
>  - From 7:00 AM UTC – 10:00 AM UTC
>  - From 4:00 PM UTC – 7:00 PM UTC
>#### July 28, 2021
>  - From 7:00 AM UTC – 10:00 AM UTC
>  - From 4:00 PM UTC – 7:00 PM UTC

- 그래서 새벽 2시의 나는 생각지도 않은 오류를 만났다고 한다.
- 비밀번호로 설정되어 있던 것을 Personal access token으로 바꿔주면 
  간단하게 해결되는데 이것저것 되는 대로 건들이다가 빙빙 돌아가서 한참 헤맸다.
- 7월 28일, 29일에도 또 있으니 참고하세요.

### 🚨 8월 13일부터는 필수적으로 토큰을 사용해야 한다!
```text
August 13, 2021 – Token (or SSH key) authentication will be required for 
all authenticated Git operations.
```


## 💡 해결 (MacOS 기준)
- 우선 Personal access token 발급받자.
  - 여기에 자세히 설명되어 있다 : [GitHub Docs - Creating a personal access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token#using-a-token-on-the-command-line)
- 기존에 비밀번호 세팅되어있는 것을 변경해주어야 한다.
- `git config --global -l`로 설정을 확인해보니 `credential.helper=osxkeychain`가 있다.
  - `키체인 접근` 실행 (⌘ + space 눌러서 검색하면 쉽게 실행 가능)
  - `github` 검색해서 더블 클릭
  - 암호 보기 체크
  - 기존 암호 지우고 위에서 발급 받은 Personal access token 입력 후 변경 사항 저장
