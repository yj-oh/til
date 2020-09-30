# Commit options

##### 커밋 (editor에서 메시지 작성)
```git
git commit
```

##### 커밋하며 인라인 형식으로 커밋메시지 입력
```git
git commit -m '{commit_message}'
```

##### 추적 중인 파일의 수정사항을 add, commit
```git
git commit -a
git commit -am '{commit_message}'
```

##### 수정 사항을 직전 커밋에 합침
```git
git commit --amend
```

##### 수정 사항을 직전 커밋에 합침 - 에디터를 띄우지 않음 
```git
git commit --amend --no-edit
```
