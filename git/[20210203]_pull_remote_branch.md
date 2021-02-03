# remote branch 가져오기
- clone을 하면 default branch만 가져온다.
- base도 제각각인 브랜치들을 어떻게 하면 제대로 가져올 수 있을까?

```git
git checkout -b <branch> <remote-branch>
```

- 만일 `dev` 브랜치를 새로 만들고 `origin/dev`를 추적하게 하려면,
```git
git checkout -b dev origin/dev
```
