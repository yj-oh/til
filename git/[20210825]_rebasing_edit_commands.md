# rebase -i 명령어들
- `rebase -i` 명령어를 사용하면 아래와 같은 주석들을 볼 수 있다.

![rebase commands](.%5B20210825%5D_rebasing_edit_commands/d6586dbc.png)

- 쓰는 것만 쓰고 있어서, 전체적으로 한 번 훑어보려고 한다.

## pick
- use commit
- 기본값. 커밋을 사용하겠다고 지정해놓은 상태.
- 커밋 순서 변경, 삭제 등의 작업 가능.
- 그대로 종료하면 아무일도 일어나지 않는다.

## reword
- use commit, but edit the commit message
- 커밋 메시지 수정
- `reword`로 지정하고 종료하면 커밋 메시지 편집창이 바로 뜬다. \
![edit](.%5B20210825%5D_rebasing_edit_commands/26d95378.png)
- 여러 개 지정했을 경우 연달아 뜬다.

## edit
- use commit, but stop for amending
- 해당 커밋 시점으로 돌아간다.
- 커밋 메시지 수정, 커밋 내용 수정 등 다양한 작업 가능.

## squash, fixup
- `squash` use commit, but meld into previous commit
- `fixup` like "squash", but discard this commit's log message
- 차이점은 합치고나서 합쳐진 애들의 커밋 메시지가 남느냐 안 남느냐.
- 우선 squash \
![squash](.%5B20210825%5D_rebasing_edit_commands/82651843.png) \
![squash2](.%5B20210825%5D_rebasing_edit_commands/63af68c1.png)
- 저장 후 log 결과를 보면 아래와 같이 page2, page3이 이전 커밋인
  page1과 합쳐지고 커밋 메시지들도 합쳐졌다.
![squash3](.%5B20210825%5D_rebasing_edit_commands/f6f89291.png)
- fixup 은 합쳐지는 애들의 메시지가 남지 않는다. \
![fixup](.%5B20210825%5D_rebasing_edit_commands/21af7b05.png)

## exec
- run command (the rest of the line) using shell
- rebase 도중에 shell 실행해준다.
- 예를 들어 아래와 같이 편집 후 저장하면, \
![exec](.%5B20210825%5D_rebasing_edit_commands/b62b482d.png)
- 이렇게 rebase 넘어가면서 순서 대로 명령어를 실행한다.
![exec2](.%5B20210825%5D_rebasing_edit_commands/a5c62a45.png)
- 어떻게 실제 활용할 수 있을지는 생각을 좀 해봐야겠다.

## break
- stop here (continue rebase later with 'git rebase --continue')
- 지정한 위치에서 멈춘다. \
![break](.%5B20210825%5D_rebasing_edit_commands/1b5e726b.png) \
![break2](.%5B20210825%5D_rebasing_edit_commands/2f550642.png)
- 어디에 쓰지...?

## drop
- remove commit
- 해당 커밋을 삭제한다.
- 해당 커밋 라인을 아예 지워버리는 것과 동일한 결과.

## label <label>
- label current HEAD with a name

## reset <label>
- reset HEAD to a label

## merge
- create a merge commit using the original merge commit's
  message (or the oneline, if no original merge commit was
  specified). Use -c <commit> to reword the commit message.
- 아래와 같이 feature/1 브랜치를 merge 하겠다고 명시하고 저장하면, \
![](.%5B20210825%5D_rebasing_edit_commands/c6cb20cc.png)
- merge commit 메시지를 편집할 수 있는 에디터 창이 뜬다. \
![](.%5B20210825%5D_rebasing_edit_commands/25134e31.png)
- 저장하면 아래와 같이 두 브랜치가 병합되고 merge commit 이 남은 걸 볼 수 있다. \
![](.%5B20210825%5D_rebasing_edit_commands/ddba2fc8.png)
- 굳이 rebase 로 이렇게 병합할 일이 있나 싶다.
