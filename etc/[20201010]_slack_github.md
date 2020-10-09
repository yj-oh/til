# Slack - GitHub 연동 설정

#### 기본 명령어
```text
/github [action] [resource]
```

#### GitHub repo 구독
```text
/github subscribe owner/repo [feature]
```

#### GitHub repo 구독 취소
```text
/github unsubscribe owner/repo [feature]
```

#### 구독 목록 확인
```text
/github subscribe list
/github subscribe list features
```

#### Features
##### 활성화
feature | description
--- | ---
issues | Opened or closed issues
pulls | New or merged pull requests, as well as draft pull requests marked "Ready for Review"
statuses | Statuses on pull requests
commits | New commits on the default branch (usually master)
deployments | Updated status on deployments
public | A repository switching from private to public
releases | Published releases

##### 비활성화
feature | description
--- | ---
reviews | Pull request reviews
comments | New comments on issues and pull requests
branches | Created or deleted branches
commits:all | All commits pushed to any branch
+label:"your label" | Filter issues, pull-requests and comments based on their labels.

##### * 자세한 내용은 : https://github.com/integrations/slack#configuration
