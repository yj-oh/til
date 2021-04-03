# Deploying JavaScript App to GitHub Pages
- 필요한 파일만 깔끔하게 배포하기

### 필요한 package 설치
```
yarn add webpack
yarn add html-loader
yarn add html-webpack-plugin
yarn add webpack-cli
```

### webpack.config.js 생성
- root
```javascript
const path = require('path');
const HtmlWebPackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './js/index.js',
    output: {
    	filename: 'bundle.js',
    	path: path.resolve(__dirname + '/build'),
    },
    module: {
    	rules: [{ test: /\.html$/, use: 'html-loader' }],
    },
    plugins: [
    	new HtmlWebPackPlugin({ template: './index.html' }),
    ],
};
```
- `entry` : 빌드할 파일
- `output` : {path}에 빌드 파일 {filename} 생성
- _참고 : [Webpack Concepts](../webpack/[20210322]_concepts.md)_

### package.json
- scripts 추가
```json
{
  "scripts": {
    "build": "webpack --config webpack.config.js"
  }
}
```

### orphan branch : gh-pages 생성
- _참고: [orphan branch - 부모 없는 브랜치 생성하기](../git/[20210317]_orphan_branch.md)_
```git
git checkout --orphan gh-pages
```
- 기존 파일 전부 삭제
```git
git rm -rf .
```
- 빈 커밋 생성, push
```git
git commit --allow-empty -m 'Init branch'

git push origin gh-pages
```

### git worktree
```git
git checkout master

echo "build/" >> .gitignore

git worktree add build gh-pages
```

### build
```
yarn build
```
```
cd build

git add .
git commit -m '{commit message}'
git push origin gh-pages
```

##### * Reference : https://medium.com/linagora-engineering/deploying-your-js-app-to-github-pages-the-easy-way-or-not-1ef8c48424b7
