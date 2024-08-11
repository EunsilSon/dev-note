# Git

### 푸시하지 않은 커밋 내역 보기
```
git log --branches --not --remotes
```

### 사용 중인 로컬 폴더를 리포지토리와 연결하기
```
git init
git remote  add origin '저장소 주소'
git pull (동기화)
```

### 브랜치 전환
```
git checkout 브랜치 명
```

### 커밋 기록/변경 사항 삭제
- staging area에서 마지막으로 커밋한 커밋 메세지 수정
```
git commit --amend
```

- 마지막 커밋 취소 (협업 시 충돌 위험 높음), 마지막 
```
git reset HEAD^
// HEAD^^ 는 커밋 2개 취소
```

<br>

`reset` 커밋 기록 + 내부 내용 **모두** 삭제 후 이전으로 되돌림  
`revert` 커밋 **기록 남음** + 커밋 내부 내용 삭제

<br>

- 모든 변경 사항 취소
```
git checkout .
```

### 최근 커밋 변경사항 확인
```
git diff
```

### 브랜치 병합
```
git checkout main
git merge 병합할 브랜치 -m "메세지"
git push
```

### 스태시 (로컬 저장소에 작업 내역 임시 저장)
```
git stash
git stash list // 저장된 내용 확인

/* stash 복원 및 삭제 */
git stash pop // list에 남지 않음
git stash apply // list에 남음
```