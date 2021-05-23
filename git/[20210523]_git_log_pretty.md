# git log --pretty
- git log 옵션 중 `--pretty`가 있다.
- 히스토리를 볼 때 정보의 양을 선택할 수 있다.

```git
git log --pretty={format}
```

- formats
  - oneline
  - short
  - medium
  - full
  - fuller

# Formats

## 👉 oneline
```text
<hash> <title line>
```

#### 예시
```text
31cbab1 [20210520]_cdn.md
```


## 👉 short
```text
commit <hash>
Author: <author>

    <title line>
```

#### 예시
```text
commit 31cbab130397c07099cabe6ae56ff9573dabf30a
Author: yj-oh <holidayoh99@gmail.com>

    [20210520]_cdn.md
```


## 👉 medium
```text
commit <hash>
Author: <author>
Date:   <author date>

    <title line>
    <full commit message>
```

#### 예시
```text
commit 31cbab130397c07099cabe6ae56ff9573dabf30a
Author: yj-oh <holidayoh99@gmail.com>
Date:   Thu May 20 19:34:39 2021 +0900

    [20210520]_cdn.md
```


## 👉 full
```text
commit <hash>
Author: <author>
Commit: <committer>

    <title line>
    <full commit message>
```

#### 예시
```text
commit 31cbab130397c07099cabe6ae56ff9573dabf30a
Author: yj-oh <holidayoh99@gmail.com>
Commit: yj-oh <holidayoh99@gmail.com>

    [20210520]_cdn.md
```


## 👉 fuller
```text
commit <hash>
Author:     <author>
AuthorDate: <author date>
Commit:     <committer>
CommitDate: <committer date>

    <title line>
    <full commit message>
```

#### 예시
```text
commit 31cbab130397c07099cabe6ae56ff9573dabf30a
Author:     yj-oh <holidayoh99@gmail.com>
AuthorDate: Thu May 20 19:34:39 2021 +0900
Commit:     yj-oh <holidayoh99@gmail.com>
CommitDate: Thu May 20 19:34:39 2021 +0900

    [20210520]_cdn.md
```

##### * Reference : https://git-scm.com/docs/pretty-formats
