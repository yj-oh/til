# log 그룹별로 요약해서 보기 - git shortlog
- https://git-scm.com/docs/git-shortlog
```git
git shortlog
```
- Author, 제목으로 그룹화한다.

![shortlog](.%5B20210826%5D_git_shortlog/cd9df985.png)

# Options
## -n, --numbered
- Author 알파벳 순서가 아닌, Author 의 커밋수로 정렬 (내림차순)
```text
yj-oh (475):
      [20200626]_webpack.md
      [20200627]_정적스코프와_동적스코프.md
      [20200628]_전역스코프와_블록스코프.md
      ...
Yunju Oh (6):
      Initial commit
      [20200625]_boot에서_JSP사용하기.md
```

## -s, --summary
- 커밋을 나열하지 않고 커밋수만 보여줌. \
![-s](.%5B20210826%5D_git_shortlog/9eecb272.png)

## -e, --email
- Author 메일 주소 표시

## -c, --committer
- Committer 로 그룹화

## -w[\<w>[,\<i1>[,\<i2>]]]
- 줄 바꿈
- 기본값 76, 6, 9

![-w](.%5b20210826%5d_git_shortlog/79be92cc.png)

- `git shortlog -w50,3,6`

![-w50,3,6](.%5b20210826%5d_git_shortlog/09dda273.png)
