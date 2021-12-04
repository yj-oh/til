# GitHub 라벨에 대해 알아보자 (& 커스텀 설정 편하게 하기)
- 참고 : [GitHub Docs - Managing labels](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels#about-labels)

## About labels
- issue, pull requests, discussions 를 분류하는 용도
- 각 repo 마다 설정할 수 있다.
- 반대로 말하면 각 repo 마다 설정해야 한다.

## Default labels
![default labels](.%5B20210714%5D_github_labels_images/4461721f.png)

| 라벨               | 설명                      | Close 기준 (이건 내 마음) |
|------------------|-------------------------|--------------------|
| bug              | 버그 수정                   | 버그 수정              |
| documentation    | 문서에 대한 개선, 추가           | 문서 업데이트            |
| duplicate        | 중복                      | 원본 링크 남김           |
| enhancement      | 새로운 기능 요청               | 구현                 |
| good first issue | 첫 기여자에게 좋은 이슈           | 해결                 |
| help wanted      | 관리자가 이슈 또는 PR에 대해 도움 요청 | 해결                 |
| invalid          | 더이상 관련 없음               | 이유 남김              |
| question         | 질문                      | 답변, 해결             |
| wontfix          | 대응하지 않을 것               | 이유 남김              |

## Custom labels
- GitHub 홈페이지에서 하는 건 [참고 링크](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels#about-labels) 에 자세히 설명되어 있다.
- 문제는 위에서도 이야기했듯이 각 repo 마다 설정해줘야 하는 듯.
- 그래서 json 파일에 정의하여 적용하는 방법을 알아보자.
- Personal access token 필요하다.
  - [GitHub Docs - Creating a personal access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token#using-a-token-on-the-command-line)
  - token scopes - repo 넣어줘야 한다.

### labels.json
- 이름이 꼭 labels 일 필요는 없다.
- `name`, `color`, `description` 정의할 수 있다.
```json
[
  {
    "name": "라벨_이름",
    "color": "Hex_code",
    "description": "라벨_설명"
  }
]
```

### 적용하기
```text
npx github-label-sync --access-token <token> --labels <json_파일명> <username>/<repo>
```

### +) 적용하다가 발생한 오류들
- 422 validation failed
  - color 에 `#` 붙여서 `#ffffff` 이런 형식으로 적음 -> code만 적을 것.
  - color 에 `red` 적음 -> 안 됨. hex code 적을 것.

---

- 컴퓨터 어디 구석에다가 라벨 세트 종류별로 정의해놓고 `npx github-label-sync`
  사용해서 repo 마다 적용하면 GitHub 에서 하나하나 설정하는 것보다 훨씬 편할 듯.
