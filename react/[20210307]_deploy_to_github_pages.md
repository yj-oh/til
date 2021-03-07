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
- 위에 설정했던 주소로 접근하면 페이지가 뜨는 걸 확인할 수 있다.
- GitHub repository - 우측 Settings - Options 들어가서 스크롤 내려보면
  GitHub Pages가 있다.
  
![](.%5B20210307%5D_deploy_to_github_pages_images/19742c3a.png)
