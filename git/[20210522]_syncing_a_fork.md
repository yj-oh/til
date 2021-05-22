# fork 해온 repository 최신 상태로 동기화하기

## ☝️ local repository 에 upstream repo 연결
```git
git remote add upstream {upstream repository}
```

## ✌️ fetch
```git
git fetch upstream
```

## 🤟 rebase 또는 merge
  - master 브랜치를 동기화한다고 가정한다
```git
git checkout master
```

### rebase
```git
git rebase upstream/master
```

### merge
```git
git merge upstream/master
```
