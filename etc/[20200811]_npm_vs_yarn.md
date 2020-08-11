# npm vs yarn

## Perfomance
- yarn이 조금 더 빠르긴 하나 큰 차이 없음

## 사용 빈도
- npm이 더 많다
![npm vs yarn](.%5B20200811%5D_npm_vs_yarn_images/a877e686.png)

## 보안
```text
One of the main reason Facebook developed Yarn was to address NPM’s security 
issues in a better way. NPM allowed packages to run code on installation 
automatically and on-the-fly, even from their dependencies automatically 
and on the fly. While this feature has its conveniences, it raised a few 
security concerns – especially considering the no-vetting registry policy 
on package submissions which we talked about early on. Conversely, Yarn only 
installs from your yarn.lock or package.json files. More specifically, yarn.lock 
ensures that the same package is installed throughout all devices, thus 
drastically reducing the chance of bugs from having different versions installed.

Since these concerns are still in force at the time of writing, I think that 
Yarn is preferable in terms of security.

* Reference : https://www.ryadel.com/en/yarn-vs-npm-pnpm-2019/
```
- 대략 facebook이 yarn을 개발한 건 npm의 보안 문제를 해결하기 위함이었고 그래서 yarn이 낫다는.

##### 이런저런 글들 찾아보는데 현재로서는 npm과 yarn이 큰 차이를 보이지는 않는다고. 마음에 드는 거 써야겠다.

---

### create package.json
```
npm init
yarn init
```

### install
```
npm install
yarn install
```

### add package
```
npm install {package name}
yarn add {package name}
```

### delete package
```
npm uninstall {package name}
yarn remove {package name}
```
