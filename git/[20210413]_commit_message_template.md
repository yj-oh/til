# Commit message template

## .stCommitMsg
- global 설정 확인
```git
git config --global --list
```
- 중간에 아래와 같은 템플릿 설정이 있다.
```text
commit.template=/Users/yjo/.stCommitMsg
```
```text
vim /Users/yjo/.stCommitMsg
```
- 열어보니 아무것도 없다.
- 찾아보니 SourceTree가 만든 파일인 듯?

## .git/COMMIT_EDITMSG  
- local project에서 무언가 커밋을 하면 하단에 이런 경로가 잡힌다.
```text
~/pj/til/.git/COMMIT_EDITMSG
```
- 열어보니 아래와 같은 템플릿이 세팅되어있다.
```text
# 변경 사항에 대한 커밋 메시지를 입력하십시오. '#' 문자로 시작하는
# 줄은 무시되고, 메시지를 입력하지 않으면 커밋이 중지됩니다.
#
# 현재 브랜치 master
# 커밋할 변경 사항:
#       수정함:        README.md
#       새 파일:       git/[20210413]_commit_message_template.md
```

## ⭐⭐⭐️️️ Custom template
- 나는 `.gittemplate` 파일을 만들기로 한다.
```text
vim ~/.gittemplate
```
```text

# [TYPE] SUBJECT
# | <------ Maximum length of subject is 70 -----------------------> |
# CONTENT

# ISSUE_TYPE : #ISSUE_NUMBER

# -------- TYPE LIST -----------------------------------------
#  [기능]     : 기능 구현
#  [추가]     : 추가
#  [수정]     : 수정, 삭제 등 기존 코드의 변경이 있음
#  [리팩토링] : 코드 리팩토링 : 기능의 변경이 없음
#  [테스트]   : 테스트 코드
#  [버그]     : 버그 수정
#  [형식]     : 주석 수정 코드 정렬 등 코드의 변경이 없음
#  [기타]     : 파일 추가 등 : 코드의 변경이 없음

# -------- ISSUE_TYPE LIST -----------------------------------
#  [해결] : 해결된 이슈
#  [관련] : 아직 해결되지 않은 이슈
#  [참고] : 참고할 이슈

# ------------------------------------------------------------
#  - [TYPE]과 SUBJECT 사이에 공백
#  - SUBJECT와 CONTENT, CONTENT와 ISSUE는 빈 줄로 구분
#  - 본문은 "어떻게"보다 "무엇을", "왜" 수정했는지 위주로 작성
# ------------------------------------------------------------
```

- `.gitconfig` 수정
```text
vim ~/.gitconfig
```
```text
[commit]
        template = /Users/yjo/.gittemplate
```
