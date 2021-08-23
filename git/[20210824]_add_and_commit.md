# add & commit
- add 와 commit 을 한 번에 하는 명령어가 있다.
```git
git commit -am "{commit_message}"
```
- 처음 명령어 알고 나서 모든 파일에 대해 add & commit 하는 줄 알았다.
- **🚨 추적하고 있던 파일의 변경 사항에 대해서만 add 한다.**
  - 새로 추가된 파일은 X

## 해결
- 고로 모든 파일을 add & commit 하고 싶다면 정석대로 아래와 같이 사용.
```git
git add .
git commit -m "{commit_message}"
```
- 아니면 단축어 등록해서 사용.
```git
git config --global alias.acmm '!git add --all && git commit -m'
```
```git
git acmm "{commit_message}"
```
- 단축어 관련 참고
  - [git 명령어 단축어 지정]([20200814]_git_명령어_단축어.md)
  - [사용하고 있는 git 단축어 모음]([20201214]_사용하고_있는_git_단축어_모음.md)
