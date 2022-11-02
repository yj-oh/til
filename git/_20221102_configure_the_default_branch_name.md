# 로컬 기본 브랜치 이름 설정하기
- 로컬에서 `git init`을 하면 `master` 브랜치가 생기는데, GitHub은 기본 브랜치를 `main`으로
  가져가고 있다.
- 그래서 세팅하게 됨.

### 설정
```shell
git config --global init.defaultBranch <name>
```

### 확인
```shell
git config --global --get init.defaultBranch
```
