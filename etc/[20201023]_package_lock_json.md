# package.json
- 프로젝트 속성, 설명, 작성자, 라이선스, 버전 정보 등을 정의한 json 형태의 파일
- 앱에 필요한 최소 버전을 기록한다.
- 패키지를 설치할 때 사용된다.
- `npm install` or `yarn install`을 하면 이 파일에 기록된 정보를 이용하여 `node_modules` 생성

## 그러나
- 패키지의 버전은 계속해서 바뀌고 의존하는 패키지에 따라서도 영향을 받으므로
최소 버전을 기록한 `package.json`만으로는 똑같은 조건의 설치가 어렵다. 

# package-lock.json
- `package.json`이나 `node_modules`가 생성, 수정될 때 자동으로 만들어짐.
- 스냅샷 방식을 통해 정확히 재현할 수 있는 node_modules 트리의 정보를 담고 있다.
- `package.json`의 종속성을 다시 계산하지 않고, `package-lock.json`에 명시된 대로 생성.
- 모든 개발자가 같은 조건 아래 개발하기 위해 필수적.
