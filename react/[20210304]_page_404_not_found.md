# 배포 후 404 Not found - AWS, Azure
- 상황은 이렇다 : [Entry point : index.html vs index.js]([20210303]_entry_point.md)
  - `/`로 접근했을 때는 문제 없이 페이지를 띄우는데,
    `/login`등 uri template 변수를 넣으면 404 error가 뜨는 상황.
  - But, `/static.html`과 같이 정적 페이지에 직접 접근하면 문제 없음.
- 그렇다는 건, `/login`으로 접근했을 때 `login.html`이 없기 때문에 not found를 띄우는 거 아닌가?
- 이렇게 시작된 서버 설정에 대한 삽질.

---

# AWS & Nginx
### Nginx .conf
```
server {
  # ...
  location / {
    try_files $uri $uri/ /index.html;
  }
}
```
- 내가 이해한 바에 따르면 위 설정은 아래와 같은 의미다.
- `http://example.com/board/profile.png`로 접근 시
  - 먼저 `profile.png` 파일을 찾음.
  - 없으면 다음으로 `/board` 폴더를 찾음.
  - 없으면 index.html을 띄움.
  - 그래도 없으면 404 error page.
- `/login`으로 접근했을 때, 해당 이름의 static 리소스가 없으므로 index.html로 가고
  이후는 리액트가 렌더링 & 라우팅 해준다.

---

# Azure
- 문제는 Azure다. 처음 써봄. 아무 지식 없음.
- 계속 404가 떨어지는데, index.html만 제대로 타도 해당 문제는 해결될 것.
- `/` 이외의 주소로 접근했을 때 index.html을 못 타는 게 문제라고 파악.
- Nginx에 설정해준 것처럼 Azure도 설정할 수 있는 게 있을 텐데. 있어야 되는데.
- 결국 찾음.
- 해당 스토리지 계정 -> 설정/정적 웹 사이트

![](.%5B20210304%5D_page_404_not_found_images/cfcf8923.png)

- 저 `오류 문서 경로`가 빈 값이었는데, index.html을 지정해줬다.
- `오류 문서 경로`에 대한 설명을 보니 아래와 같다.

![](.%5B20210304%5D_page_404_not_found_images/50c0a7a6.png)

- 이렇게 싱겁게 해결됨. 🤷‍♀️
