# 코드 스타일 통일을 위한 Prettier - IntelliJ 설정

### 👉 package 설치
```
npm install prettier
yarn add prettier
```

### 👉 WebStorm Plugin `Prettier` 설치
- Preferences (MacOS 단축키 `⌘,`) - Plugins
![WebStorm Plugin Prettier](.%5B20201104%5D_prettier/5d723635.png)

### 👉 `Prettier` 설정
- Preferences - Languages & Frameworks - javascript - Prettier
   - package 설치된 node_modules 내의 prettier 폴더를 `Prettier package`에 지정해줌
- on code reformat, on Save 체크 (저장할 때마다 자동 format)
![Languages & Frameworks](.%5B20201104%5D_prettier/ee553d6a.png)

## ⭐️ .prettierrc
#### project root 경로(src, package.json 등이 있는)에 .prettierrc 생성
- 아래 설정은 대표적으로
   >- printWidth 80
   >- 세미콜론 `true`
   >- singleQuote `true`
   >- tab, size 4
- 등등을 넣어놨다.
```prettier
{
  "arrowParens": "always",
  "bracketSpacing": true,
  "htmlWhitespaceSensitivity": "css",
  "insertPragma": false,
  "jsxBracketSameLine": false,
  "jsxSingleQuote": true,
  "printWidth": 80,
  "proseWrap": "preserve",
  "quoteProps": "as-needed",
  "semi": true,
  "singleQuote": true,
  "useTabs": true,
  "tabWidth": 4,
  "trailingComma": "all"
}
```
##### * Options : https://prettier.io/docs/en/options.html
##### * Prettier config editor : [https://prettier.io](https://prettier.io/playground/#N4Igxg9gdgLgprEAuEAzArlMMCW0AEAEnADYkQDqEATiQCYAUwA5tXHLlM-gLz4A6IABalyggDT5W7eHV74A5IKq06ghZIDOOEghjzUAQxKa4k6AFkI6UwHkAbnGriAvgEp8wflG-58OVAYAQmkOHC43YDYYdGoofCh0MhcAbm9fPz8Aeiz8ABVbABFbJHxC6AV9Gzh8akMoOggAW394tganDN19RJa+C0MYIQA6VHIafAYBoeG6huaGDwAqfABGAFEAagB2N2GYCABlGGpw5kXZuAAHEkMwOAYs-n5h57pNrJxmSUFBN3T4rUOLF4gAeOg4ez4MC3TSaAByhiacB4CmIZEoNHoCnwuBguh4wAABgBNaz4QxsfD2HDaA7UBLoJoAIyc+AAJMBGS0XESXPhLNY7I5qITBdUHE4XAA+AGZfCgzQnaDMaVc0KcZjDTQkHD3Bj4AAMklW+D2BwAqlcrk4AMKGUyLfCbKRsMJcbW6-Wrc0QAAyEAA7naHQ8PC5QVkldQVbLAX4WG7NcMEHRNBQcEMGBI-vgAPwCECF-ClRVXer4JUATwJwGAkHI1FKSn40irChcMokhcjmnLUGl+BcGT8oLgTTj-Bg6qTcDkw58MEj47j8q5DG0ulg-3jmQLgleIBHmVKgiCggXx8jEPs0rSPigLhA4hAECuuGgmmQoEpMcDAAVKQQL8UGMQNDCrL8X2ZOowAAaw4Q5yzAM5kBOdAzBAcdWToOg5z9epmHQQxmDgAAxGgmkGTVkBAQx0AOZ9hBgJoSAoIRMzgPs7jgQ5gMzSFMyrWiwDhJjwlMagYH-OpmCo5AjBMTCACtNAADwAIVghCYEOJE4D9cI4AU4xTBfVS1MOM5dAARXQCB4DQ6gMJfctqEk2jmUMVkSCYq5TlgDM6CGZAAA5jRAfyIFMCg6iuWj-K4pxHCYgBHez4Bkt8QLozQAFooHYPC6CYth0pwNgZJI+SkEUsyQFMJocCclyGusuA7Ic4ykHQzCYG8oKQqQAAWF8TkMHQzltZoaqwzQAFYmOqPJvJAurMPsDCAEkOlgQ4wFOd8AEEGmOGtuvWzsgA)

---

- 2020.11.26 수정
    - title, 파일명 수정
    - file watchers 사용하지 않음
    - Prettier 설정 : on code reformat, on Save 설정 정보 추가
    - `.prettierrc` 옵션 내용 수정
