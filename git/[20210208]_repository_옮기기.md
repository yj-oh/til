# repository 옮기기
- `test`라는 repository를 그대로 `test2` repository에 복사해 놓고 싶다.
- 로컬에 `test` 폴더가 있는 상황.

## 방법 1
- 기존 폴더 `test`를 복사
```git
cp -r test test2
```
- remote 주소 변경
```git
git remote set-url origin https://github.com/yj-oh/test2.git
```
- remote push
```git
git push origin master
```

## 방법 2
- 찾아보니 엄청 간단한 방법이 있다.
```git
git push --mirror https://github.com/yj-oh/test2.git
```
- 마압소사...
- 근데 생각해보니 폴더 복사해서 remote 새로 연결하고 푸시하는 것이나,
  새로 푸시하고 그걸 로컬에 다시 땡겨오는 거나 거기서 거기 아닌가 싶은.
- 상황에 따라 적절한 방법을 사용하자.

---

### 2021.02.24 추가
- `push --mirror` 했다가 새로운 repository에 있던 젠킨스 파일을 날려먹었다.
- 로컬이면 복구할 방법이 있었을 텐데 remote라 젠킨스 파일 다시 만들어달라고 팀원에게 부탁함.
- 새삼스러운 교훈 : remote에 적용하는 명령어는 조심 또 조심하자.
