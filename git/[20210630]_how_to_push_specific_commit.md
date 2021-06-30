# 특정 커밋까지만 Push 하기
- 로컬에 작업한 커밋이 잔뜩 있는데 전부 push 하지 않고, 특정 커밋까지만 push 하고 싶을 때.
```git
git push {remote_name} {commit_hash}:{remote_branch_name}
```

### Ex.
```git
git push origin a1b2:master
```
