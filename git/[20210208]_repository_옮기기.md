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
