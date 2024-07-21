---
order: 6
title: Interlock
date: 2023-07-22
categories: [AI Dev. Env., GIT]
tags: [Dev. Env., DVCS, GIT]
math: true
image:
  path: /_post_refer_img/GIT/Thumbnail.png
---

## Interlock Local & Remote
-----

![01](/_post_refer_img/GIT/06-01.jpg){: width="100%"}

### Search

```
git remote <OPTION>
```

- `remote` : 원격 저장소와 관련된 작업에 사용하는 명령어

- `<OPTION>`
    - `None` : 로컬 저장소에 연결되어 있는 원격 저장소의 별명을 조회함
    - `-v` : 로컬 저장소에 연결되어 있는 원격 저장소의 별명 및 경로를 조회함

### Interlock

```
git remote add <NICKNAME> <REMOTE-REPO-PATH>
```

- `remote add` : 로컬 저장소에 원격 저장소를 연결함

- `<NICKNAME>` : 호출 시 사용할 원격 저장소 별칭
    - `upstream` : 최상위 원격 저장소
    - `origin` : 여러 개의 원격 저장소를 위계를 세워 연동하지 않는 한 통상 해당 이름을 사용함
    - `alt`

- `<REMOTE-REPO-PATH>` : 연결할 원격 저장소의 경로

### Rename

```
git remote rename <EXISITING-NAME> <NEW-NAME>
```

- `remote rename` : 원격 저장소 별명을 `<EXISITING-NAME>` 에서 `<NEW-NAME>` 으로 변경함

### Change

```
git remote set-url <NICKNAME> <NEW-PATH>
```

- `remote set-url` : `<NICKNAME>` 에 할당되어 있는 원격 저장소 경로를 변경함

### Reset

```
git remote remove <NICKNAME>
```

- `remote remove` : `<NICKNAME>` 에 할당되어 있는 원격 저장소와의 연결을 해제함

## DownLoad Remote Repository
-----

![02](/_post_refer_img/GIT/06-02.jpg){: width="100%"}

### 복제하기

```
git clone <OPTION> <REMOTE-REPO-PATH>
```

- `clone` : 원격 저장소의 커밋 내역을 가져와서 로컬에 새로운 저장소를 생성함

- `<OPTION>`
    - `None`
    - `-b <BRANCH-NAME>` : 특정 브랜치만 복제함
    - `--single-branch -b <BRANCH-NAME>` : 특정 브랜치만 복제 후 해당 브랜치만 추적함
    - `--depth <N>` : 최신 커밋 `HEAD` 로부터 특정 깊이까지만 복제함

### 가져와서 병합하기

```
git pull <OPTION> <NICKNAME> <BRANCH-NAME>
```

- `pull` : 원격 저장소의 커밋 내역을 가져와서 로컬 저장소의 내역과 병합함

- `<OPTION>`
    - `None` : `fetch` + `merge`
    - `-r` : `fetch` + `rebase`

### 가져와서 임시 분기하기

```
git fetch <OPTION> <NICKNAME> <BRANCH-NAME>:<NEW-NAME>
```

- `fetch` : 원격 저장소의 커밋 내역을 가져와서 브랜치명 `<NEW-NAME>` 으로 임시 분기한 상태로 열람함
    - `<NEW-NAME>` 을 별도로 지정하지 않으면 `FETCH_HEAD` 로 자동 설정함

- `<OPTION>`
    - `None`
    - `--dry-run` : 원격 저장소의 커밋 내역을 로컬로 가져오지 않고, 가져올 것이 있는지 여부만 확인
    - `--all` : 원격 저장소의 모든 브랜치에 대한 내역을 가져옴

## Upload Local Changes to Remote
-----

![03](/_post_refer_img/GIT/06-03.jpg){: width="100%"}

### Push

```
git push <OPTION> <REMOTE-NICKNAME> <REMOTE-BRANCH-NAME>
```

- `push` : 로컬 브랜치의 커밋(변경 확정 내역)을 원격 브랜치에 반영함

- `<OPTION>`
    - `None`
    - `--all` : 모든 로컬 브랜치에 대하여 기능함
    - `--tags` : 모든 로컬 태그에 대하여 기능함
    - `--force` : 충돌 시 경고를 무시하고 강제로 기능함
    - `--dry-run` : 실제로 푸시하지 않고 어떤 변경 사항이 발생할지 미리 확인함

### Tracking

```
git push --set-upstream <REMOTE-NICKNAME> <REMOTE-BRANCH-NAME>
```

- `push --set-upstream` : 현재 체크인한 로컬 브랜치를 원격 저장소 `<REMOTE-NICKNAME>` 의 브랜치 `<REMOTE-BRANCH-NAME>` 에 연동함

-----

### Reference

- [Git - 간편 안내서](https://rogerdudler.github.io/git-guide/index.ko.html)
- [누구나 쉽게 이해할 수 있는 Git 입문](https://backlog.com/git-tutorial/kr/)