## error "The engine "node" is incompatible with this module."
- package install 하는데 에러가 남
```text
yjoui-MacBookPro-15:react-redux-boilerplate yjo$ yarn install
yarn install v1.22.4
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
error postcss@8.1.3: The engine "node" is incompatible with this module. 
Expected version "^10 || ^12 || >=14". Got "13.12.0"
error Found incompatible module.
info Visit https://yarnpkg.com/en/docs/cli/install for documentation 
about this command.
```
- node `13.12.0`란다.
- 업그레이드 필요하다.

```
brew update
brew upgrade node
```
- 확인
```
node -v
v15.3.0
```
