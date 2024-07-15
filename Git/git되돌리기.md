# Git 되돌리기

[Git revert 재설정](#git-revert-재설정)

[revert한 commit 이름 설정](#revert한-commit-이름-설정)

[Git reset 되돌리기](#git-reset-되돌리기)

[파일 내용 수정 전으로 되돌리기](#파일-내용-수정-전으로-되돌리기)

[Staging Area -> Working Drectory](#staging-area---working-drectory)

---

## Git revert 재설정

```bash
git rever <commit id>
```

> - commit id는 4자리 이상부터 인식 가능
> 
> - 없었던 일로만 처리되고 commit이 사라지는 건 아님
> 
> - 여러 커밋 한번에 실행 취소
>   
>   - 공백 사용 `d338 658f`
>   
>   - `..`로 범위 지정

---

## revert한 commit 이름 설정

1. 명령 모드 -> 입력 모드

```bash
i
```

2. 입력 모드 -> 명령 모드

```bash
ESC KEY
```

3. **저장 및 나가기**

```bash
:wq
```

> - **기본 commit message 쓰려면 `:wq`만 사용**
> 
> - **편집기 안 열려면 `git revert --no--edit <commit id>`**
> 
> - 자동 commit 안하고 Staging Area에만 올리려면
>   
>    `git revert --no--commit <commit id>`

---

## Git reset 되돌리기

- staging area에 남김

```bash
git reset --soft <commit id>
```

- **working directory에 남김 (기본 옵션)**

```bash
git reset --mixed <commit id>
```

- commit의 기록을 남기지 않음 (위험!)

```bash
git reset --hard <commit id>
```

> `git reflog`로 조회하여 `git reset`으로 복구가능

---

## 파일 내용 수정 전으로 되돌리기

- 파일 수정 전으로 되돌리기

```bash
git restore 파일명
```

> 복구 불가능

---

## Staging Area -> Working Drectory

- commit이 없는 상태에서만 사용 가능

```bash
git rm --cached 파일
```

- git 저장소에 commit이 존재하는 경우

```bash
git restore --staged 파일명
```
