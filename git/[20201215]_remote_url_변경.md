# remote url 변경
- repository 이름이 바뀌어서 재설정하려고 한다.
```git
git remote remove origin
git remote add origin {new url}
```
- 물론 이렇게 기존 remote 연결을 해제하고 다시 새로운 remote를 연결하는 방법도 있겠지만
한 번에 할 수는 없을까?
  
## 💡 git remote set-url
```git
git remote set-url origin {new url}
```
