# Prettier options
- 현재 진행하고 있는 리액트 프로젝트에서 사용할 prettier 옵션을 정리 중.
- 쓸 때 쓰더라도 알고 쓰자.
* 함께 보기 : [코드 스타일 통일을 위한 Prettier - IntelliJ 설정]([20201104]_prettier_intellij_설정.md)
* Reference : https://prettier.io/docs/en/options.html

```text
{
  "arrowParens": "always",              // 화살표 함수 괄호 <always | avoid>
  "bracketSpacing": true,               // 대괄호 사이의 공백 <bool>
  "htmlWhitespaceSensitivity": "css",   // html 공백 민감도 <css | strict | ignore>
  "insertPragma": false,                // @format marker 사용 여부 <bool>
  "jsxBracketSameLine": false,          // jsx의 > 위치 <bool>
  "jsxSingleQuote": true,               // jsx의 작은 따옴표 사용 여부 <bool>
  "printWidth": 80,                     // 인쇄 너비 <int>
  "proseWrap": "preserve",              // 마크다운의 줄바꿈 <always | never | preserve>
  "quoteProps": "as-needed",            // 객체 속성의 따옴표 방식 <as-needed | consistent | preserve>
  "semi": true,                         // 세미콜론 사용 여부 <bool>
  "singleQuote": true,                  // 작은 따옴표 사용 여부 <bool>
  "useTabs": true,                      // 탭 사용 여부 <bool>
  "tabWidth": 4,                        // 들여쓰기 탭 너비 <int>
  "trailingComma": "all"                // 여러 줄일 때 후행 콤마 <es5 | none | all>
}
```

### arrowParens
- 화살표 함수 괄호
- 괄호를 생략하는 것이 얼핏 심플해보일 수 있지만 추가, 수정이 더 어려워질 수도 있음을 알고 있을 것.

option | description | example
--- | --- | ---
always | 항상 괄호 포함 | (x) => x
avoid | 가능하면 괄호 생략 | x => x

### bracketSpacing
- 대괄호 사이의 공백

option | description | example
--- | --- | ---
true | 공백 O | { foo: bar }
false | 공백 X | {foo: bar}

### htmlWhitespaceSensitivity
- html 공백 민감도
- 인라인 요소에서 공백은 중요하므로 공백 구분 형식을 지정토록 한다.

option | description | example
--- | --- | ---
css | CSS `display` 속성의 값을 따름 | 
strict | sensitive. | {foo: bar}
ignore | insensitive. | {foo: bar}

### insertPragma
- 파일이 prettier로 포맷되었음을 알리는 @format marker를 파일 상단에 삽입
- `<bool>`

### jsxBracketSameLine
- jsx의 `>` 위치
- true
    ```jsx
    <button
      className="name"
      onClick={handleEvent}>
      저장
    </button> 
    ```
- false
    ```jsx
    <button
      className="name"
      onClick={handleEvent}
    >
      저장
    </button> 
    ```

### jsxSingleQuote
- jsx의 작은 따옴표 사용 여부
- `<bool>`

### printWidth
- 인쇄 너비
- `<int>`
- 가독성을 위해 80자 이상 사용하지 않는 것을 권유

### proseWrap
- 마크다운의 줄 바꿈

option | description | example
--- | --- | ---
always | 항상 wrapping | 
never | wrapping 하지 않음 | 
preserve | 그대로 둔다 | 

### quoteProps
- 객체 속성의 따옴표 방식 <as-needed | consistent | preserve>

option | description | example
--- | --- | ---
as-needed | 필요할 때만 추가 | 
consistent | 일관되게 적용 | 
preserve | 입력된 대로 둔다 | 

### semi
- 세미콜론 사용 여부
- `<bool>`

### singleQuote
- 작은 따옴표 사용 여부
- `<bool>`

### useTabs
- 탭 사용 여부
- `<bool>`

### tabWidth
- 들여쓰기 탭 너비
- `<int>`
- 기본은 2

### trailingComma
- 여러 줄일 때 후행 콤마

option | description | example
--- | --- | ---
es5 | ES5 (객체, 배열 등) | 
none | 후행 콤마 없음 | 
all | 함수 인수 포함, 가능한 경우 후행 콤마 입력 | 
