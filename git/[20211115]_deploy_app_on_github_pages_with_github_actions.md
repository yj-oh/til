# GitHub Actions 이용하여 GitHub Pages 배포 자동화하기
- GitHub Actions 에 대한 대략적인 설명 : `TIL` [Quickstart for GitHub Actions]([20211114]_quickstart_for_github_actions.md)

---

# yaml 파일 생성
- `.github/workflows`
- yaml 파일 이름 자유.
```yaml
# Workflow 이름. GitHub Actions 페이지에 보임.
name: Build & Deploy

# 필수. trigger.
on:
  # push 이벤트가 발생하면 실행됨.
  push:
    # 단, main 브랜치에서만.
    branches:
      - main

# 실행할 작업
jobs:
  # 작업 이름 (키워드 아님. 원하는 이름으로 지을 수 있다. 이 작업 이름은 'deploy')
  deploy:
    # 작업을 실행할 machine type
    runs-on: ubuntu-latest
    # 작업의 세부 단계. name 을 보면 무슨 작업인지 알 수 있으니 따로 설명은 하지 않는다.
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      # https://github.com/actions/setup-node
      - name: Setup Node
        uses: actions/setup-node@v2
        with:
          node-version: 16.x

      - name: Installing dependencies
        run: npm install

      - name: Building App
        run: yarn run build

      # https://github.com/peaceiris/actions-gh-pages
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          # build 결과물이 생성되는 파일 이름을 명시한다.
          publish_dir: ./public
```

# Commit, Push
- GitHub Actions page
- 좌측에 보면, yaml 파일에 적어주었던 `name`인 'Build & Deploy' 가 `Workflows`에 보인다.
![GitHub Actions page](.%5b20211115%5d_deploy_app_on_github_pages_with_github_actions_images/79e4fdfb.png)
- 'deploy' 는 yaml 파일에 적어주었던 `jobs.{name}`이다.
- 해당 작업 눌러보면,
![GitHub Actions page2](.%5b20211115%5d_deploy_app_on_github_pages_with_github_actions_images/a1790040.png)
- step 에 명시해준 각 세부 작업들이 순서대로 실행된 것을 볼 수 있다.
- 각각 클릭하면 세부 log 확인할 수 있다.
![GitHub Actions page - detail](.%5b20211115%5d_deploy_app_on_github_pages_with_github_actions_images/186098c0.png)
