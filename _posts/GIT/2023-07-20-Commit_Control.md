---
order: 4
title: Commit Control
date: 2023-07-20
categories: [AI Dev. Env., GIT]
tags: [Dev. Env., DVCS, GIT]
math: true
image:
  path: /_post_refer_img/GIT/Thumbnail.png
---


## Search
-----

### Commit History

```
git log <OPTION>
```

- `log` : 현재 위치한 브랜치의 커밋 내역을 조회함

- `<OPTION>`
    - `None` : 현재 위치한 브랜치의 커밋 히스토리 조회
    - `--stat` : 파일별 변경 사항 히스토리 조회
    - `--oneline` : 커밋 해시 및 주석 목록 조회

### Commit

```
git show <COMMIT-HASH>
```

- `show` : 특정 커밋의 정보를 상세 조회함

- `<COMMIT-HASH>`
    - `None` : `HEAD` 커밋

### Difference
    
```
git diff <COMMIT-1>..<COMMIT-2>
```

- `diff` : 커밋 간 변경 사항의 차이점을 조회함

- `<COMMIT-1>..<COMMIT-2>` : `<COMMIT-1>` 에만 존재하는 변경 사항

## Move
-----

- **커밋 전환의 이해**

    ![01](/_post_refer_img/GIT/04-01.jpg){: width="100%"}

    - 커밋을 이동하는 것은 변수 `HEAD` 가 가리키는 커밋을 변경하는 작업임

- **변수 `HEAD` 의 이해**

    ![02](/_post_refer_img/GIT/04-02.jpg){: width="100%"}

    - 변수 `HEAD` 는 현재 체크인하고 있는 브랜치를 가리키고, 각 브랜치는 마지막 커밋을 가리킴
    - 즉, 변수 `HEAD` 는 현재 체크인하고 있는 브랜치를 참조하여 마지막 커밋을 간접으로 가리키게 됨

- **DETACHED HEAD**

    ![03](/_post_refer_img/GIT/04-03.jpg){: width="100%"}

    - **정의** : `HEAD` 가 브랜치를 참조하지 않고 커밋을 직접 가리키는 상태

    - **문제점**
        - 이동한 커밋에서 새로운 커밋을 생성하면 해당 커밋은 브랜치를 벗어나 단독으로 존재하는 상태가 됨
        - 본래 커밋은 직접 지목되지 않고 브랜치를 참조하여 지목되므로 해당 커밋을 가리킬 방법이 없음
        - 이러한 경우 새로운 커밋에서 시작하는 새로운 브랜치를 생성하여 해결함
    
### refer. Commit Hash
    
```
git switch <COMMIT-HASH>
```
    
### refer. Tag
    
```
git switch tags/<TAG-NAME>
```

## Copy & Paste
-----
    
### Paste
    
```
# 커밋을 붙여넣을 브랜치로 이동
git switch <BRANCH-NAME>

# 커밋 붙여넣기
git cherry-pick <COMMIT-HASH>
```

- `cherry-pick` : 현재 위치한 브랜치에 특정 커밋을 기록함

### If Conflict
    
```
# 충돌 사항 수정 후 해당 파일들을 스테이지에 올리기
git add <conflict files>

# 일시중지 작업에 대하여 재개 혹은 중단
git cherry-pick <OPTION>
```
    
- `<OPTION>` : 일시중지 작업에 대하여 기능함
    - `--continue` : 작업 재개
    - `--abort` : 작업 중단 및 일시중단 이전 상태로 복원

## Cancel
-----

### 커밋 되돌리기

![04](/_post_refer_img/GIT/04-04.jpg){: width="100%"}

```
git revert <COMMIT-HASH>
```
 
- `revert` : 특정 커밋 상태로 되돌리는 새로운 커밋을 생성함

### 커밋 삭제하기

![05](/_post_refer_img/GIT/04-05.jpg){: width="100%"}

```
git reset <OPTION> <COMMIT-HASH>
```
    
- `reset` : 특정 커밋 이후에 추가 기록된 커밋들을 모두 삭제하고 해당 커밋으로 되돌림

- `<OPTION>`

    ![06](/_post_refer_img/GIT/04-06.jpg){: width="100%"}

    - `--hard` : `HEAD` 를 해당 커밋으로 되돌리고, 파일의 `modified` 및 `staged` 상태를 해제하고, 해당 커밋 이후에 기록된 커밋을 삭제함
    - `--mixed` : `HEAD` 를 해당 커밋으로 되돌리고, 파일의 `modified` 및 `staged` 상태를 유지하되, 해당 커밋 이후에 기록된 커밋을 삭제함
    - `--soft` : `HEAD` 를 해당 커밋으로 되돌리되, 파일의 `modified` 및 `staged` 상태를 유지하고, 해당 커밋 이후에 기록된 커밋을 유지함

-----

### Reference

- [Git - 간편 안내서](https://rogerdudler.github.io/git-guide/index.ko.html)
- [누구나 쉽게 이해할 수 있는 Git 입문](https://backlog.com/git-tutorial/kr/)