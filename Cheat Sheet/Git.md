# Git 명령어 정리

#### 푸시하지 않은 커밋 확인
```
git log --branches --not --remotes
```

#### 로컬 폴더를 Git 리포지토리와 연결
```
git init
git remote add origin '저장소 주소'
git pull   # 원격과 동기화
```

#### 브랜치 전환
```
git checkout 브랜치명
```

#### 마지막 커밋 메시지 수정
- 푸시하지 않은 커밋 메시지 수정 가능
- 푸시한 커밋을 amend하면 해시가 변경되어 원격에서는 새로운 커밋으로 인식
```
git commit --amend
```

#### 마지막 커밋 취소
```
git reset HEAD^
```
- HEAD^ → 마지막 1개 커밋 취소
- HEAD^^ → 마지막 2개 커밋 취소
- 협업 시 주의: 이미 푸시된 커밋을 reset하면 충돌 위험 있음
  
**커밋 내용 완전히 되돌리기 vs 기록 남기기**
- reset → 커밋 기록 + 내부 내용 모두 삭제, 이전 상태로 되돌림
- revert → 커밋 기록 남기면서 커밋 내부 내용 삭제

#### 모든 변경 사항 취소
```
git checkout .
```

#### 최근 커밋 변경 사항 확인
```
git diff
```

#### 브랜치 병합
- 병합 후 충돌이 생기면 수동 해결 필요
```
git checkout main
git merge 병합할브랜치 -m "메시지"
git push
```

#### 스태시 (작업 임시 저장)
```
git stash            # 현재 작업 임시 저장
git stash list       # 저장된 스태시 확인
git stash pop        # 복원 후 스태시 목록에서 제거
git stash apply      # 복원 후 스태시 목록 유지
```

#### 브랜치 이름 변경 및 원격 처리
```
# 로컬 브랜치 이름 변경
git branch -m old-branch new-branch

# 새 브랜치를 원격에 등록
git push origin new-branch

# 원격의 기존 브랜치 삭제
git push origin --delete old-branch
```
