# GitHub에서 merge 충돌 해결
- 회사 동료가 겪었던 문제를 같이 알아보고 고민하다가 알게 된 사실을 정리한다.
  
## 상황
- master 브랜치에 dev 브랜치를 합치려고 함.
- 내 프로젝트는 아니라서 잘 모르지만 내부 정책 상 feature 브랜치를 dev 브랜치에 병합할 때 
  리뷰를 하기 때문에 해당 병합은 따로 리뷰를 하지 않았나 봄.
- dev 브랜치의 변경사항을 push 하고 github 에서 PR을 생성한 뒤 self merging.
- conflict 나서 충돌난 코드 잘 정리하여 merge 커밋 남김.

![](https://docs.github.com/assets/images/help/pull_requests/merge-conflict-commit-changes.png)  

## 문제의 시작
- master 브랜치에 있는 변경사항 중 dev 병합되면 안 되는 것이 있었는데
  배포 병합 후 확인하니 dev에 그 변경사항이 반영되어버림. (자동 배포 설정되어 있음)
- 뭘까 하고 히스토리 추적.
- 내 프로젝트는 아니라 풀 땡겨서 히스토리 보는데 기절할 뻔함.

![](.%5B20210319%5D_resolving_a_merge_conflict_on_github_images/6ff2a592.png)

- 멘붕의 시작.
- 깃을 쓰면서 한 번도 이런 히스토리를 본 적이 없어서 어떻게 봐야하는지부터 감을 잡아야 했다.
- 하루종일 히스토리만 눈빠지게 봤다.
- 결국 정리한 사실은 매우 단순.

## 원인
![](.%5B20210319%5D_resolving_a_merge_conflict_on_github_images/82bc6ded.png)

- 충돌을 해결하고 `Commit merge`를 했는데, 
  충돌난 파일 외 포함되어서는 안 될 변경사항이 해당 커밋에 섞여있었고
  깃헙이 그걸 dev 브랜치에 커밋 해버렸다.
  
```text
Warning: When you resolve a merge conflict on GitHub, 
the entire base branch of your pull request is merged into the head branch. 
Make sure you really want to commit to this branch. 
If the head branch is the default branch of your repository, 
you'll be given the option of creating a new branch to serve 
as the head branch for your pull request. If the head branch is 
protected you won't be able to merge your conflict resolution into it, 
so you'll be prompted to create a new head branch. For more information, 
see "About protected branches."
```
_* Reference : https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-on-github_

- 정리하면
  - 깃헙에서 충돌을 해결하면 pull request base branch가 head branch로 병합된다.
    - 위의 상황에서는 base branch = master, head branch = dev
  - 그러니 정말 커밋할 건지 확인해라.
  - head branch가 막혀있으면 충돌 해결한 걸 병합할 수 없으니 
    새 head branch 를 생성하라는 메시지를 준다.

## 해결 방법
1. 리뷰 없이 단순히 병합만 할 용도라면 푸시 후 깃헙에서 병합하는 게 아니라
   로컬에서 병합 후 푸시.
   - 깃헙은 위의 `원인`에서 이야기한 규칙을 가지고 있지만, 로컬에서 병합할 경우
     더 자유롭게 상황 컨트롤 가능.
   - 푸시 후 병합, 병합 후 푸시, 단순한 순서의 차이.
2. 무언가 병합되면 안 될 규칙을 가지고 있는 프로젝트라면,
   자동 배포까지 걸려있는 중요한 브랜치를 보호 설정 해놓거나 철저한 리뷰 정책도 함께 세울 것.
3. 아니면 병합되면 안 될 무언가를 커밋에 남기지 말고, .gitignore에 포함시킨 뒤 해당 내용 따로 관리할 것.

## 교훈
- 내가 깃 히스토리에 집중하는 이유는, 히스토리가 직관적이지 않고 잘 관리되어 있지 않으면
  이런 문제 상황에서 원인을 파악할 때 몇 배의 시간과 고생이 들기 때문이다.
  - 문서 작업과 정리와 기록을 중요하게 생각하는 이유도 같다.
- 적어도 내가 참여하는 프로젝트는 몇 명의 개발자가 몇 개의 브랜치를 사용하든
  예술 작품 같은 히스토리를 남기지 않겠다고 새삼스럽게 다짐.
  - 그러기 위해 더 많은 공부와 케이스를 접하는 것이 필요하겠다.
- 자칭 깃덕후지만 깃에 거부감을 가진 개발자들의 마음이 이해가 된다.
- 정말 단순하게 쓰려면 그렇게 쓸 수도 있고, 
  잘 쓰려면 높은 자유도를 가지고 무궁무진하게 원하는 대로 쓸 수 있다는 게 깃의 많은 장점 중 하나지만 
  그렇기 때문에 프로젝트를 진행할 때 명확한 규칙을 잡아놓는 게 중요하겠다.
- 깃을 너무 좋아해서 우스개소리로 "나는 진성 깃 덕후다" 하고 다니는데 
  개발자 각각이 내가 생각해본 적도 없는 방법으로 다양하게 깃을 사용하는 걸 보고,
  그리고 그 과정에서 생긴 문제를 가지고 헬프를 요청해서 같이 고민할 때마다
  깃에 대해 아직 모르는 게 많다는 걸 매번 느낌.
- 온전히 깃에만 집중하고 있었는데 깃헙은 또다른 문제였다.
- 동료들이 다양한 케이스의 문제들을 많이 질문해줬으면 좋겠다.
