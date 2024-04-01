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

### 최근 add 되돌리기
```
git reset head
```

### 최근 커밋 되돌리기
```
git revert 커밋 로그
```

### 브랜치 전환
````
git checkout 브랜치 명
```