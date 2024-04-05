# JPA (Java Persistance API)
- Java ORM 기술에 대한 API 표준 (인터페이스 모음)
- 구현체를 이용해 구현 (Hibernate 등)
- 객체 중심 개발이 가능해 생산성 증가 및 유연한 유지 보수

<br>

### ORM (Object-Relational Mapping)
- 객체와 RDB의 테이블 간의 매핑을 자동화하는 기술
- 객체와 테이블간의 구조와 표현 방식의 불일치 해결 (패러다임 일치)
- Java 언어로 DB를 다룸

<br>

# 장점
- Hibernate는 SQL을 직접 사용하지 않고, 메서드를 호출해 자동 쿼리 수행
- 유연한 유지 보수
- DBMS에 종속적이지 않음

<br>

# 단점
- 직접 SQL을 호출하는 것보다 성능이 떨어질 수 있음
- 복잡한 쿼리 사용이 어려움
- 학습 비용 증가

<br>

# MyBatis
- **개발자가 작성한 SQL**을 Java 메서드와 매핑 시켜줌 (SQL문은 XML 파일로 저장)
- 복잡한 쿼리 및 SQL 제어가 필요한 경우 사용

<br>

### 왜 우리나라는 MyBatis 사용량이 JPA보다 더 높을까?
- Google Trend
![google_trend](https://github.com/EunsilSon/dev-note/assets/46162801/238d8320-db0e-4b90-81cd-3ffc533c8477)

JPA는 복잡한 쿼리를 사용하기 어렵고, MyBatis는 개발자가 원하는 대로 SQL을 작성할 수 있다.  우리나라 시장 대부분이 SI 또는 금융 시장이기 때문에 **복잡한 비즈니스와 안정성을 중요시 하는 서비스의 경우 SQL을 자동 생성하는 것보다 직접 작성하는 것이 좋다고 생각된다.** 
최근, 서비스 기업에서는 JPA를 많이 사용하는 추세라고 한다.