# WebStorm Live Template 설정

## Preferences 
##### MacOS 단축키 : `⌘` `,`
![](.%5B20200831%5D_webstorm_live_template_images/382cddec.png)

- Editor - Live Templates
- 오른쪽 `+` 버튼 클릭
- Abbreviation, Description, Template text 입력
- 변수는 `$변수명$`과 같은 형태로 작성

```javascript
// 이미지 속 코드
import React from 'react';
import styled from 'styled-components';

const $fileName$Block = styled.div``;

const $fileName$ = () => {
    return (
    	<$fileName$Block>

    	</$fileName$Block>
    );
};

export default $fileName$;
```

## Live template variables
- 라이브 템플릿 변수에 함수를 사용할 수 있다.
- [참고] https://www.jetbrains.com/help/webstorm/template-variables.html

##### 만약 확장자를 제외한 파일명을 변수로 사용하고 싶다면,
- 상단 이미지에 파란 네모 친 `EDIT VARIABLES` 버튼 클릭
![](.%5B20200831%5D_webstorm_live_template_images/a73690fd.png)
- `fileName`이라는 변수에 `fileNameWithoutExtension()`의 반환값을 사용한다는 것.
   - `fileNameWithoutExtension()`: Returns the name of the current file without its extension.
   
## 사용해보기
- AuthTemplate.js 파일 생성
- 위에서 설정한 단축어 입력
![](.%5B20200831%5D_webstorm_live_template_images/032f6236.png)

- 엔터키를 누르면 아래와 같이 자동으로 템플릿이 입력됨 \
![](.%5B20200831%5D_webstorm_live_template_images/d11a2915.png)
