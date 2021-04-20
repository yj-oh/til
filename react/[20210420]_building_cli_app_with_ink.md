# Building CLI application with Ink
```text
mkdir ink-example
cd ink-example
```
```text
npx create-ink-app

// or

npx create-ink-app --typescript
```

![](.%5B20210420%5D_building_cli_app_with_ink_images/b72e5385.png)

- `ink-example` 명령어를 날리면 위와 같이 `Hello, Strange`가 출력된다.

## 👉 TypeScript 사용하기
- 타입 스크립트를 사용할 때에는 몇 가지 설정이 필요했다.

### cli.tsx
```tsx
import App from './ui';

// 위를 아래로 변경

import App from './ui.js';
```

### tsconfig.json
```json
{
  "compilerOptions": {
    "moduleResolution": "node",
    "target": "ES6",
    "module": "commonjs"
  }
}
```
- `compilerOptions` 컴파일 시 적용되는 옵션들
- `moduleResolution` 컴파일러가 import가 무엇을 참조하는지 알아내기 위해 사용하는 프로세스
- `target` 어떤 버전으로 컴파일 할 것인지
- `module` 어떤 모듈 방식으로 컴파일 할 것인지

## 👉 프로젝트를 clone 받은 뒤 실행이 되지 않는다면
```text
yjoui-MacBookPro-15:ink-example yjo$ ink-example
-bash: ink-example: command not found
```

- 프로젝트 빌드
```text
npm run build

or 

yarn build
```

- 글로벌 설치
```text
npm install --global
```
