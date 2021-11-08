# Local & Remote branch 이름 변경
- 어떤 프로젝트는 디폴트 브랜치가 `master`, 어떤 프로젝트는 `main`이다.
- 이전에 생성한 애들은 `master`, 최근 생성한 애들은 `main`
- 일단 푸시 들이대고, 거부 당하면 다시 푸시하는 일이 반복되어 모든 브랜치를 `main`으로 바꾸기로 한다.
  - 바로 이 프로젝트도.

---

# ⭐️ 결론
```git
git branch -m {old-branch} {new-branch}
```
```git
git push origin :{old-branch} {new-branch}
```
```
git fetch -p origin
```

---

## 브랜치 이름 변경
```git
git branch -m {old-branch} {new-branch}
```

## Push
```git
git push origin :{old-branch} {new-branch}
```

## ...🚨 에러!!!
```text
yjo@yjoui-MacBookPro til % git push origin :master main
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'main' on GitHub by visiting:
remote:      https://github.com/yj-oh/til/pull/new/main
remote:
To https://github.com/yj-oh/til.git
 * [new branch]      main -> main
 ! [remote rejected] master (refusing to delete the current branch: refs/heads/master)
error: 레퍼런스를 'https://github.com/yj-oh/til.git'에 푸시하는데 실패했습니다
```
- remote 에 master 와 main 이 공존한다.
  - GitHub 에서 확인하면 main 브랜치 뿐인데 local 에서 `git branch -a`로 확인하면 둘 다 보인다.
- 강제로 master 브랜치만 없애본다.
```
git push origin :master
```
```
error: unable to delete 'master': remote ref does not exist
error: 레퍼런스를 'https://github.com/yj-oh/til.git'에 푸시하는데 실패했습니다
```

## 💡 해결
- 로컬과 원격지의 어긋남.
- fetch 해준다.
```
git fetch -p origin
```
