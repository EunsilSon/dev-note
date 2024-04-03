# Spring Container
- 자바 객체(Bean)의 인스턴스화, 구성, 생명 주기 및 제거 관리
- 생성된 자바 객체들에게 추가적인 기능 제공

<br>

## Spring Container 사용 이유
객체 생성을 위해서 new 생성자를 사용할 시, 애플리케이션에서는 많은 객체가 존재하고 서로를 참조하게 된다.  
객체 간의 참조가 많으면 의존성이 높아진다.
따라서, **객체 간의 의존성을 낮춰 결합도를 낮추고 높은 캡슐화를 위해 Spring Container를 사용한다.**

<br>

## Spring Container 종류
![container](https://github.com/EunsilSon/dev-note/assets/46162801/75608ada-0031-4c78-8730-f3a1e54bb23f)

- Beanfactory와 ApplicationContext 두 종류의 인터페이스로 구현
    - Beanfactory는 Bean의 생성과 관계설정 같은 제어를 담당하는 IoC 오브젝트
    - ApplicationContext는 IoC 방식에 따라 만들어져 Beanfactory를 확장한 것으로, **주로 사용되는 Spring Container**

<br>

## Beanfactory
- Spring Container의 최상위 인터페이스
- Bean 등록, 생성, 조회
- getBean() 메서드를 통해 Bean 인스턴스화
- @Bean 어노테이션이 붙은 메서드의 이름을 Spring Bean의 이름으로 사용해서 Bean 등록

<br>

## ApplicationContext
- Beanfactory의 기능을 상속받아 부가 기능 제공

<br>

## Spring Container 생성과 등록
### 1. 어노테이션 기반
```java
@Configuration
public class AppConfig {

    @Bean
    public MemberService memberService() {
        return new MemberServicelmpl(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```
Spring Container가 @Configuration 이 붙은 클래스를 설정 정보로 사용 → **객체 DI**
    - 클래스 내부에 @Bean 이 붙은 메서드를 모두 호출해 얻은 객체를 Container에 등록
    - 등록된 객체를 Spring Bean 이라고 함

```java
public class MemberApp {
    public static void main(String[] args) {
        ApplicationContext applicationContext = new AnnotaionConfigApplicationContext(AppConfig.class); // Container 생성
        MemberService memberService = applicationContext.getBean("memberService", MemberService.class);
    }
}
```
- ApplicationContext를 Spring Container라고 하며, 인터페이스로 구현됨
- 다형성이 적용되어 있고, 다양한 구현체가 존재
    - 사용한 구현체: `AnnotaionConfigApplicationContext`
- `applicationContext.getBean("이름", 타입)` 메서드를 사용해 Bean을 얻을 수 있음

<br>

### 2. XML 기반 메타데이터의 기본 구조
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
        
    <bean id="..." class="...">  
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions go here -->
</beans>
```
- `<beans />` 필요한 값들을 설정
- `<bean id="…">` Bean 정의 식별
- `<bean class="…">` Bean 유형 정의 및 클래스 이름 사용