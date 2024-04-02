# Spring의 특징
![spring_1](https://github.com/EunsilSon/dev-note/assets/46162801/df5073b7-d79f-4a33-8666-8a5816a32cd4)

## 1. POJO (Plain Old Java Object)
- 이후에 주로 특정 자바 모델이나 기능, 프레임워크 등을 따르지 않은 **순수 자바 오브젝트**
- 특정 환경에 종속적이지 않아야 한다.
- 객체지향적인 설계를 제한없이 적용할 수 있다.

<br>

## 2.1 IoC(Inversion of Control) 제어의 역전
- **스프링 자체에서 객체의 생명 주기를 관리**해 필요한 객체를 생성하지 않아도 된다.
- 메서드나 객체의 호출작업을 외부에서 결정

> 1. 객체 생성
> 2. 의존성 객체 주입 (스프링이 만들어 놓은 객체를 외부에서 주입)
> 3. 의존성 객체 메서드 호출
> Bean 생성 → 스프링이 실행될 때 생성되고, 필요한 곳에 주입시켜준다. 컨테이너 내 싱글톤으로 관리

<br>

## 2.2 DI(Dependency Injection) 의존성 주입
- `@Autowired` 어노테이션을 사용해 스프링 컨테이너에 있는 빈을 주입해 객체 생성
- 계층이나 서비스 간의 **의존성을 자동으로 연결**
- OCP (Open-Closed Principle) : 변경에는 닫힘 확장에는 열림

>1. Setter (메서드 주입)
>2. Field Injection (필드 주입)
>3. **Contructor injection (생성자 주입) → Spring 권장**
    - 객체 불변성 확보 가능
    - 테스트 용이
    - final 키워드와 Lombok을 활용해 간결한 작성
    - 순환 참조 에러 방지

<br>

## 3. AOP(Aspect Oriented Programming) 관점 지향 프로그래밍
- 핵심 관점(Core concern)과 부가 관점(Cross-cutting concern)으로 로직을 나눠, 관점을 기준으로 모듈화해 핵심에만 집중할 수 있게 한다.
- 프로그램의 변경과 확장에 유연한 대처 가능
- 코드 간결성 유지
- 코드 재사용

<br>

## 4. PSA(Portable Service Abstraction)
- 추상화 계층을 사용해 어떤 기술을 내부에 숨기고 개발자에게 편의성을 제공하는 **서비스 추상화**
- 애플리케이션 요구 사항 변경에 유연한 대처 가능
- ex) Spring Web MVC, Spring Transaction, Spring Cache, JDBC, JPA 등