# GitHub pages 배포
- create-react-app 이용해서 프로젝트를 만들었다.
- repository 생성하고 local과 remote 연결하고 등등은 생략.

### package 설치 : `gh-pages`
```
npm install gh-pages

or

yarn add gh-pages
```

### package.json
- `homepage`, `scripts.predeploy`, `scripts.deploy` 추가
```json
{
  "homepage": "http://{username}.github.io/{repository name}",
  "scripts" : {
    "predeploy": "yarn run build",
    "deploy": "gh-pages -d build"
  }
}
```

### 명령어 실행
```
npm run deploy

or

yarn run deploy
```

### 확인
- `gh-pages`라는 브랜치가 remote에 자동으로 생성되었을 것이다.
  
  ![](../git/.%5B20210317%5D_orphan_branch_images/44181724.png)
  
- 위에 설정했던 주소로 접근하면 페이지가 뜨는 걸 확인할 수 있다.
- GitHub repository - 우측 Settings - Options 들어가서 스크롤 내려보면
  GitHub Pages가 있다.
  
![](.%5B20210307%5D_deploy_to_github_pages_images/19742c3a.png)

## +)
- gh-pages 브랜치는 뭐지?
- 왜 부모 커밋 없이 혼자 동동 떠있지?
- 직접 생성하려면 어떻게 해야 하지?
- 가 궁금하다면 아래 링크 참고.
  - [orphan branch - 부모 없는 브랜치 생성하기](../git/[20210317]_orphan_branch.md)
