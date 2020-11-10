## 💁‍♀️ 이전 편 : [git checkout -b <new_branch> \[\<start point\>\]]([20201109]_connot_lock_ref.md)
# test repository 
- 모든 테스트는 `yj-oh/test`에 있는 코드로 실시한다.
- clone을 떴다. 
- 아무것도 하지 않으면 아래와 같은 상태다.

![sourcetree](.%5B20201111%5D_cannot_lock_ref2/fb6a0d8b.png)

## 💻 test
#### 👉 test 프로젝트는 아래와 같은 디렉토리 구조를 가진다.
    - .git 폴더 내부에 refs 폴더가 있다.
        - refs 폴더 내부에 heads, remotes, tags 폴더가 있다.

![](.%5B20201111%5D_cannot_lock_ref2/4efe44c3.png)

#### 👉 펼치면 아래와 같다.
```text
|-- apple1.txt
|-- apple2.txt
|-- dev1.txt
|-- dev2.txt
|-- page1.html
|-- page2.html
|-- page3.html
|-- README.md
|-- .git
|   |-- hooks
|   |   `-- {...}
|   |-- info
|   |   `-- exclude
|   |-- logs
|   |   |-- refs
|   |   |   `-- {...}
|   |   `-- HEAD
|   |-- objects
|   |   `-- {...}
|   |-- 📂 refs
|   |   |-- 📂 heads
|   |   |   |-- 📄 apple
|   |   |   |-- 📄 dev
|   |   |   `-- 📄 master
|   |   |-- 📂 remotes
|   |   |   `-- 📂 origin
|   |   |       `-- 📄 HEAD
|   |   `-- 📂 tags
|   `-- {...}
`-- build.gradle
```
- (Emoji가 붙은 아이들만 살펴볼 것이다.)

#### 👉 중점적으로 볼 refs 폴더 내부 파일들의 내용은 아래와 같다.
### 📄 .git/refs/heads/apple
- apple2 의 SHA-1
```text
6e4efece9784bec660135a4a26da209e582889da
```

### 📄 .git/refs/heads/dev
- dev2 의 SHA-1
```text
7deb4132883b734411ed9aec0331531bf34eae64
```

### 📄 .git/refs/heads/master
- page3 의 SHA-1
```text
af31fc5a623d621c8d75f11624dd774495320a6e
```

### 📄 .git/refs/remotes/origin/HEAD
```text
ref: refs/remotes/origin/master
```

---

## default 상태를 파악했으니 마음껏 주물주물 해보자.
- 설명은 `git log`로 되어 있지만, 심플하게 파악하기 위해 실제 사용한 명령어는 `log --pretty=oneline`임을 미리 밝힌다.

```git
git log {SHA-1}
```
- 위 명령어를 통해 해당 SHA-1 값을 가지는 커밋과 그 이전의 커밋 히스토리를 조회할 수 있다.
- master의 마지막 커밋을 기준으로 히스토리를 조회해보자.
![](.%5B20201111%5D_cannot_lock_ref2/cdc1d6d7.png)
- 하지만 매번 이런 식으로, 외우기 어려운 SHA-1 값을 이용해 로그를 조회할 수는 없는 일이다.
- 쉬운 이름으로 된 포인터가 있으면 좋겠다.
- 그 포인터는 이미 존재한다.
- 명령어 `git log af31` 대신 `git log master`를 사용해보자.
![](.%5B20201111%5D_cannot_lock_ref2/4998ed2d.png)
- 동일한 히스토리가 문제 없이 조회된다.
- 어떻게 이게 가능할까? 무엇이 포인터의 역할을 하고 있을까?

```
echo "181fe5ed30a2bd0c5ecc33df530f3efc95daa188" > .git/refs/heads/master
```
- `181fe5ed30a2bd0c5ecc33df530f3efc95daa188`라는 내용을 가진 `.git/refs/heads/master`를 생성한다.
- 이미 파일이 존재하면 내용을 교체한다.
- 위의 명령어를 실행하고 cat 명령어로 해당 파일의 내용을 확인해보면, 아래와 같다.
![](.%5B20201111%5D_cannot_lock_ref2/c99650fc.png)
- 내용이 `af31...`에서 `181f...`로 수정되었다.
- `git log master`를 확인하면?
- `master`가 page2 커밋으로 이동했다.
![](.%5B20201111%5D_cannot_lock_ref2/acc1a4a0.png)

### .git/refs/heads/master가 가지고 있는 SHA-1 값이 포인터 역할을 하고 있다는 걸 알 수 있다.
### 하지만 숨겨져 있는 Refs의 파일을 직접 고치는 것은 적절하지 않다. 안전하게 수정하는 방법은?
### 이때 `git update-ref` 명령어가 등장한다.
- `181f` 커밋의 이전 커밋인 `9006`을 가리켜보자.
```git
git update-ref refs/heads/master 9006
```
![](.%5B20201111%5D_cannot_lock_ref2/bf2514fe.png)
- `echo` 명령어를 이용해서 숨겨져있는 파일을 직접 수정하지는 않았지만 동일한 이펙트를 냈다.
### update-ref 명령어는 이런 이유 때문에 존재한다.

## `git branch {branch_name}`이 등장한다.
- 해당 명령어를 실행하면 git은 내부적으로 update-ref 명령을 실행한다.
- 입력받은 브랜치 이름과 현 브랜치의 마지막 커밋의 SHA-1 값을 가져다 update-ref 명령을 실행한다.
- 이 말인 즉슨, \
![](.%5B20201111%5D_cannot_lock_ref2/bf2514fe.png)
- 이 상태에서 `git branch master2` 명령어를 실행하면 
- git이 내부적으로 `git update-ref refs/heads/master2 9006` 명령어를 실행한다는 말이다.
- 진짜 그런지 확인해보자.
- 우선 `git branch master2`를 실행한다.
![](.%5B20201111%5D_cannot_lock_ref2/b59364ba.png)
- `master2` 파일이 새로 생성되었다.
- 내부를 살펴보면 `9006...` 값이 들어있을 것이다.
![](.%5B20201111%5D_cannot_lock_ref2/f1f48c23.png)
- 빙고
- 로그를 찍어보자.\
![](.%5B20201111%5D_cannot_lock_ref2/bf2514fe.png)
- 이 상태에서 `master2`가 추가되었을 것이다.
![](.%5B20201111%5D_cannot_lock_ref2/dd9c73e7.png)
- 빙고
- 다시 초기화했다.

## 또다시 등장한다 `git checkout -b {branch_name}` (-b 옵션이 붙었다.)
- 이 명령어는 아래와 같이 동작한다. 
    - git branch {branch_name} + git checkout {branch_name}
    - 그리고 위의 명령어는 또다시 아래와 같이 동작한다.
        - git update-ref refs/heads/{branch_name} {마지막 커밋의 SHA-1} + git checkout {branch_name}

- 그러므로
- `master` 브랜치의 마지막 커밋 `af31`에서
- `git checkout -b new`를 실행하면
```git
git update-ref refs/heads/new af31
git checkout new
```
- 가 실행될 것이다.
- .git/refs/heads 아래에 새롭게 new 파일 생성되고, 내부에는 `af31...` 값이 저장되어 있을 것이다.
![](.%5B20201111%5D_cannot_lock_ref2/2ee82c02.png)
- ㄴ `new` 브랜치가 생성되었다. \
![](.%5B20201111%5D_cannot_lock_ref2/da9f4eb7.png)
- ㄴ .git/refs/heads 아래에 새롭게 new 파일 생성되었다.
![](.%5B20201111%5D_cannot_lock_ref2/3f9576f7.png)
- ㄴ new 파일 내부에 `af31...` 값이 저장되었다.
- 빙고
- 다시 초기화했다.

## 그럼 `git checkout -b new`가 아니라 `git checkout -b new origin/apple/dev`를 실행하면?
- git update-ref refs/heads/new af31
- git checkout new
- 근데 start_point가 `origin/apple/dev`이므로
![](.%5B20201111%5D_cannot_lock_ref2/d6bb397b.png)
- ㄴ 이 상태에서
![](.%5B20201111%5D_cannot_lock_ref2/8518abbb.png)
- ㄴ 이렇게 되고
- .git/refs/heads 아래에 새롭게 new 파일 생성되고
- new 파일 내부에 `6e4e...` 값이 저장될 것이다.
![](.%5B20201111%5D_cannot_lock_ref2/fa9d3d20.png)
- ㄴ `6e4e` 커밋을 베이스로 삼은 `new` 브랜치가 생성되었다. \
![](.%5B20201111%5D_cannot_lock_ref2/e9b3ff4f.png)
- ㄴ .git/refs/heads 아래에 새롭게 new 파일 생성되었다.
![](.%5B20201111%5D_cannot_lock_ref2/4632095b.png)
- ㄴ new 파일 내부에 `6e4e...` 값이 저장되었다.
- 빙고
- 다시 초기화했다.

## 그럼 git checkout -b apple/dev origin/apple/dev 는?
- git update-ref refs/heads/apple/dev 6e4e
- git checkout apple/dev
1. `6e4e` 커밋을 베이스로 삼은 `apple/dev` 브랜치가 생성될 것이다.
2. .git/refs/heads 아래에 새롭게 apple/dev 파일이 생성될 것이다.
3. apple/dev 파일 내부에 `6e4e...` 값이 저장될 것이다.

### But
- 1번의 `apple/dev` 브랜치가 생성되지 못한다.
- 이후는 당연히 실행되지 않겠지?

### git checkout -b apple/dev origin/apple/dev 말고 직접 하나하나 명령어를 날려보자.
### 1. git update-ref refs/heads/apple/dev 6e4e (실패)
```text
fatal: update_ref failed for ref 'refs/heads/apple/dev': 
cannot lock ref 'refs/heads/apple/dev': 'refs/heads/apple' exists; 
cannot create 'refs/heads/apple/dev'
```
![](.%5B20201111%5D_cannot_lock_ref2/7c55101a.png)
- ㄴ 이런 상태다. apple은 파일이기 때문에 apple의 하위 dev를 가질 수 없다.
- `apple/dev` 브랜치는 생성되지 않는다.
- `git stash`로 확인해도 아무런 변경사항이 없고, 초기화 상태다.
- 여기서 멈추지 않고 새 파일이 생성되는 걸 보면, 1번 명령어의 성공/실패와 상관없이 2번 명령어를 실행하는 듯.
- 2번을 실행해보겠다.

### 2. git checkout apple/dev
![](.%5B20201111%5D_cannot_lock_ref2/562989a4.png)
- 문제는 여기서 발생한다.
- apple/dev 브랜치는 1번에서 실패해서 존재하지 않기 때문에 checkout을 했을 때 갈 수 없다.
![](.%5B20201111%5D_cannot_lock_ref2/199f3b8e.png)
- ㄴ 일반적인 경우라면 위와 같은 error가 뜨면서 아무런 변화가 일어나지 않는다.
- 근데 변화가 일어났다. 새 파일이 생겼다. 왜?
- 다시 초기화 상태에서 1번 명령어를 실행하고 모든 상태와 파일 내부의 값을 확인했지만 바뀌는 것이 없었다.
### 그렇다면 열쇠는 2번 명령어인 `git checkout apple/dev`에 달려있다.
- 위 명령어를 실행하면
- `git checkout -b apple/dev origin/apple/dev` 명령어를 실행했을 때와 같은 에러를 만날 수 있다.
![](.%5B20201111%5D_cannot_lock_ref2/e5b071f8.png)
![](.%5B20201111%5D_cannot_lock_ref2/3cd3b3ee.png)
- 새 파일도 똑같이 생기고.
- `git checkout apple/dev`를 실행시켰을 때 .git 파일에서 변경되는 파일은 `index` 밖에 없다.
- 그리고 `index` 파일을 실행시키려고 하면 아래와 같은 경고창이 뜬다.
![](.%5B20201111%5D_cannot_lock_ref2/65ef313b.png)
- 다음 시간에는 `index`를 파헤쳐보겠다.
