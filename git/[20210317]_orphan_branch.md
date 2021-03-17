# orphan branch - 부모 없는 브랜치 생성하기
- 부모 없는, 히스토리 없는 브랜치 생성하고 checkout 하는 명령어
```git
git checkout --orphan {branch_name}
```

![git checkout --orphan](.%5B20210317%5D_orphan_branch_images/4ee935d6.png)

- 아직 아무런 커밋도 없어서 `git branch --all`을 해도 표시되지 않는다.
- `git status`를 찍어보면 베이스가 되는 브랜치의 파일들이 추적하지 않는 상태로
  stage에 올라가 있다.

![](.%5B20210317%5D_orphan_branch_images/f2dcddc8.png)

- 기존 브랜치와 전혀 상관 없는 브랜치를 만들 것이기 때문에 기존 파일들은 전부 삭제한다.
  - `git rm -rf .`
- 아무 파일이나 생성해서 커밋하고, 다시 `git branch --all`을 찍어보면 orphan 브랜치가 보인다.

![](.%5B20210317%5D_orphan_branch_images/b09dfc48.png)

- 기존 브랜치와 상관 없이 홀로 동동 떠있다.

# +) orphan branch 를 알게 된 경로
- GitHub pages를 이용해 정적 웹을 띄웠다.
  - [GitHub pages 배포](../react/[20210307]_deploy_to_github_pages.md)
- 세팅하고 `yarn run deploy`를 하면 `gh-pages`라는 브랜치가 하나 생성된다.

![](.%5B20210317%5D_orphan_branch_images/44181724.png)

- 그리고 해당 repository - settings의 GitHub Pages를 보면 아래와 같이 기본 세팅이 되어있다.

![](.%5B20210317%5D_orphan_branch_images/b330ecff.png)

- 뭔가 싶어서 Source의 Branch를 master로 바꾸고 `Save`
  
![](.%5B20210317%5D_orphan_branch_images/97f5c38b.png)

- 브랜치도 바꿨겠다, 부모 없이 동동 떠있는 `gh-pages` 브랜치는 더 필요 없겠지 싶어서 삭제.

- 그랬더니 해당 주소의 웹에 index.html이 아닌 README.md가 뜸.

![](.%5B20210317%5D_orphan_branch_images/f6e8c4fa.png)

- 다시 `yarn run deploy`를 했지만 `gh-pages` 브랜치가 생성되지 않음.
  - 원래는 자동으로 다시 생성된다. 아마 일시적으로 꼬였던듯.
- 수동으로 `build` 결과물만 담고 있는 브랜치를 생성하기 위해 찾아보다가
  orphan branch 의 존재와 의미를 알게 되었다.

## 위의 현상 해결은
- orphan branch `gh-pages` 생성
```git
git checkout --orphan gh-pages
```
- 딸려오는 파일들 전부 삭제
- master branch의 코드를 build 하고 결과물인 `build` 폴더 내부 파일을 root 폴더로 꺼내서 커밋
- remote에 push
- local branch `gh-pages` 삭제
- 해당 repository - settings의 GitHub Pages - Source - Branch를 다시 `gh-pages`로 변경
- 그럼 README.md 대신 다시 index.html이 뜬다.
