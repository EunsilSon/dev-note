# JPA 영속성 컨텍스트 (Persistence Context)
- 애플리케이션과 DB 사이에서 객체를 보관하는 가상의 데이터베이스 역할
- 엔티티 매니저를 통해 영속성 컨텍스트에 접근 가능

<br>

## 엔티티 생명 주기
![persistence_context](https://github.com/EunsilSon/dev-note/assets/46162801/bb105eb8-30ac-4fee-b682-05202ea7bd96)

- 비영속 (new/transient) : 영속성 컨텍스트와 전혀 관계 없음 
    - 객체는 생성했으나 영속성 컨텍스트에 저장하지 않은 상태  

      `Member member = new Member()`

- 영속 (managed) : 영속성 컨텍스트에 저장  
    - 엔티티 매니저를 통해 엔티티를 영속성 컨텍스트에 저장해 관리  

      `entitymanager.persist(member)`

- 준영속 (detached) : 영속성 컨텍스트에 저장되었다가 분리  
    `entitymanager.detach(member)` : 준영속 상태로 만듦  
    `entitymanager.clear()`  
    `entitymanager.close()`  
    > 영속성 컨텍스트가 제공하는 모든 기능이 동작하지 않음  
  (1차 캐시, 쓰기 지연, 변경 감지, 지연 로딩)

- 삭제 (removed)  
`entitymanager.remove(member)`

<br>

### 1. 1차 캐시
- 영속성 컨텍스트 내부에 있는 캐시
- 영속 상태의 엔티티를 저장
- 엔티티 값 조회 시 영속성 컨텍스트에 값이 있으면 반환하고, 없으면 DB에서 조회해 1차 캐시에 저장 후 반환
- 빠른 조회 가능

<br>

### 2. 쓰기 지연 (transcational write-behind)
- 쿼리를 모았다가 트랜잭션 커밋할 때 한 번에 실행
- DB 부담 최소화

<br>

### 3. 변경 감지
- 트랜잭션 커밋 시 변경을 자동 감지해 DB 자동 반영
- `영속` 상태의 엔티티에게만 적용

<br>

### 4. 지연 로딩
- 실제 DB를 사용할 때만 데이터 조회
- 프록시를 사용해 데이터를 잘못 로딩하는 문제 예방 / 비용 절약

<br>

### 5. 플러시 (flush)
- 영속성 컨텍스트의 변경 내용을 DB에 반영해 동기화시킴
    - 플러시 방법  
    1. entitymanager.flush()
    2. 트랜잭션 커밋 시 자동 호출
    3. JPQL 쿼리 실행 시 자동 호출
        