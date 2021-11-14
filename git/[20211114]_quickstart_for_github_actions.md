# Quickstart for GitHub Actions
- [GitHub Docs - Quickstart for GitHub Actions](https://docs.github.com/en/actions/quickstart)
- [GitHub Docs - Workflow syntax](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions)

---

# yaml 파일 생성
- `.github/workflows`
- 파일 이름 자유. 나는 `main.yml`로 생성
- 아래는 `GitHub Docs - Quickstart for GitHub Actions`에 나와있는 예제.
```yaml
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v2
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```

## name
- workflow 의 이름
- GitHub repo - Actions 페이지에 표시될 이름이다. \
![name](.%5B20211114%5D_quickstart_for_github_actions_images/6ccafdda.png)

## on
- 필수
- 트리거 하는 GitHub 이벤트 이름
- [GitHub Docs - Events that trigger workflows](https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows)

### Using a single event
```yaml
# push 이벤트가 발생할 때 트리거
on: push
```
### Using a list of events
```yaml
# push 또는 pull_request 이벤트가 발생할 때 트리거
on: [push, pull_request]
```
### Using multiple events with activity types or configuration
```yaml
on:
  # main 브랜치에 push 이벤트 발생 시 트리거
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
```

## jobs
- workflow 는 순차적 or 병렬도 실행되는 하나 이상의 작업으로 구성됨.
- 기본적으로 병렬 작업.

```yaml
# 보기 쉽도록 위의 예제를 떼어내 가져왔다
jobs:
  Explore-GitHub-Actions:   # 작업 이름
    runs-on: ubuntu-latest  # 작업을 실행할 machine type
    steps:                  # 작업의 각 단계
      - run:                # command 실행
      - name:               # 표시될 이름
        uses:               # 사용할 액션 (GitHub 마켓플레이스에 제공된 것이나 현재 repo 에서 만든 것 등)
```

# commit, push
