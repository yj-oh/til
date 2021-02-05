# reset options
- 커밋 되돌릴 때 `git reset --soft`, `git reset --hard`는 자주 쓰는데
  `--mixed` 옵션도 있길래 뭔가 했더니.
- 정리하는 김에 reset 옵션 전부 정리.

## 실습
![git log](.%5B20210205%5D_reset_mixed/2f848c2f.png)

## --soft
```git
git reset --soft HEAD^
```
![--soft](.%5B20210205%5D_reset_mixed/108bba4b.png)
- HEAD를 옮긴다.
- index나 워킹 디렉토리는 그대로 두고.
- 파일이 staging area에 남아있다.

## --mixed
```git
git reset --mixed HEAD^
```
![--mixed](.%5B20210205%5D_reset_mixed/1932ca1f.png)
- HEAD를 옮기고 index를 HEAD가 가리키는 상태로 만든다.
- 파일이 staging area에서 내려왔다.

## --hard
```git
git reset --hard HEAD^
```
![--hard](.%5B20210205%5D_reset_mixed/77c6325d.png)
- 워킹 디렉토리까지 업데이트 한다.
- 커밋도 되돌려지고 남아있는 변경사항도 없다.
