---
order: 3
title: File Control
date: 2023-03-08
categories: [AI Dev. Env., GIT]
tags: [Dev. Env., DVCS, GIT]
math: true
image:
  path: /_post_refer_img/GIT/Thumbnail.png
---

## `staged` 파일 임시 저장하기
-----

![01](/_post_refer_img/GIT/03-01.jpg){: width="100%"}

### 임시 저장 목록 조회하기

```
git stash list 
```

- `stash list` : 임시 저장 목록을 조회함

### 변경 사항 임시 저장하기

```
git stash save
```

- `stash save` : `staged` 파일의 변경 사항을 확정하지 않고 임시 저장함

### 임시 저장 항목 불러와서 적용하기

```
git stash apply <STASH-NAME> <OPTION>
```
  
- `stash apply` : 임시 저장 항목을 `HEAD` 커밋에 불러와서 적용함

- `option`
    - `None` : 임시 저장 항목을 불러와서 `HEAD` 커밋과 병합한 후 변경 사항을 스테이지 영역에 추가함
    - `--index` : `HEAD` 커밋과 병합 시 충돌 사항을 조회함

### 임시 저장 항목 삭제하기

```
git stash drop <STASH-NAME>
```

- `stash drop` : 특정 임시 저장 항목을 삭제함

```
git stash clear
```

- `stash clear` : 임시 저장 목록을 초기화함

## 파일 상태 다루기
-----

### .gitignore

```
WORKING-DIRECTORY-PATH/.gitignore
```

- `.gitignore` : 워킹 디렉토리 하위 항목 중 `Git` 의 추적에서 제외할 항목을 설정하는 파일

### rm

```
git rm <OPTION> <FILE-NAME>
```

- `rm` : 파일을 삭제하거나 추적에서 제외함

- `<OPTION>`
  - `None` : 파일을 삭제함
  - `--cached` : 파일을 `untracked` 상태로 전환하고 워킹 디렉토리에서는 삭제하지 않음
  - `-r` : 워킹 디렉토리의 하위 항목을 모두 삭제함
  - `--dry-run` : 명령어 실행 시 어떤 파일들이 삭제될 것인지 조회함

### 파일 상태 복원하기

```
git restore <OPTION> <FILE-NAME>
```

- `restore` : 파일 상태를 특정 시점으로 복원할 때 사용하는 명령어
  - 커밋을 이동하는(변수 `HEAD` 의 아규먼트를 변경하는) 작업이 아니므로 `detached HEAD` 를 초래하지 않음
  - 단, `restore` 상태에서 커밋 생성 시 `detached HEAD` 발생함

- `<OPTION>`
  - `None` : 파일 상태를 `HEAD` 시점으로 복원함
  - `--worktree` : `modified` 파일의 상태를 `HEAD` 시점으로 복원함
  - `--staged` : `staged` 파일의 상태를 `HEAD` 시점으로 복원함
  - `--source=<COMMIT-HASH>` : 파일 상태를 특정 커밋 시점으로 복원함

-----

### Reference

- [Git - 간편 안내서](https://rogerdudler.github.io/git-guide/index.ko.html)
- [누구나 쉽게 이해할 수 있는 Git 입문](https://backlog.com/git-tutorial/kr/)