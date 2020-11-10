# git checkout -b <new_branch> \[\<start point\>\]

## 상황
- 아래와 같은 브랜치들이 있다. \
![branches](.%5B20201109%5D_connot_lock_ref_images/ebe46d42.png)

- 전체 이력을 그래프로 보면 아래와 같다. \
![](.%5B20201109%5D_connot_lock_ref_images/b8c07df1.png)

- 이 상황에서 `git checkout -b apple/dev origin/apple/dev` 명령어를 사용하면 실패한다.
```
fatal: cannot lock ref 'refs/heads/apple/dev': 'refs/heads/apple' exists; 
cannot create 'refs/heads/apple/dev'
```

- 그래프는 아래와 같이 된다. \
![](.%5B20201109%5D_connot_lock_ref_images/2924b9da.png)

- `master` 브랜치에서 명령어를 날렸고, `git status`를 통해 변경 사항을 확인하면 아래와 같다. 
- `master` 를 베이스로 한 `dev`, `apple`의 파일들이 새로운 파일로 생성되어버렸다.
![stash](.%5B20201109%5D_connot_lock_ref_images/b59df26e.png)

## 오류 이유
- `git checkout -b apple/dev origin/apple/dev`의 정체
```git
git checkout -b|-B <new_branch> [<start point>]
```
- `origin/apple/dev`를 시작점으로 하여
- `apple/dev` 라는 브랜치를 생성하고 checkout 
- 그러나 로컬에 `apple`이라는 브랜치가 있다.
#### **⭐️ `a`라는 브랜치가 있으면 `a/b`와 같이 하위 구조를 갖는 브랜치를 생성할 수 없음.**
- 그래서 `apple/dev`를 생성하는 과정에서 실패.

## 근데 새 파일이 생성된 이유는 뭘까?
- 해당 명령어를 실행할 때에 깃이 동작하는 방식을 조금 더 들여다봐야 할 듯하다.

## 💁‍♀️ 조금 더 들여다본 내용을 정리한 다음 편 : [refs]([20201111]_cannot_lock_ref2.md)
