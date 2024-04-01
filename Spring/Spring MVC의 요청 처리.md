# Spring MVC의 요청 처리
![spring-mvc-1](https://github.com/EunsilSon/TIL/assets/46162801/adee3bb9-00e9-4430-be62-2ee72ec38a5f)

1. 요청이 들어온다.
2. Handler Mapping을 호출해 핸들러를 선택한다. (컨트롤러 메서드를 찾는 과정)
3. Handler Adapter에게 Controller 호출 권한을 위임한다.
4. Handler Adapter이 Controller를 호출한다.
    - 호출된 Controller가 비즈니스 로직 실행
5. 결과값인 Model이 생성되고 선택한 View의 이름을 반환한다.
6. View Resolver에서 View 객체를 찾아 실제 View로 만든다.
7. DispatcherServlet이 View를 반환한다.  
<br>
    **Handler Mapping, Handler Adapter, View Resolver는 모두 DispatcherServlet이 호출한다**

<br>

# DispatcherServlet 
- Spring MVC 요청 처리의 핵심
- 요청 처리를 위한 구성 요소들을 호출하는 Front Controller

<br>


# Handler Mapping
- 우선순위에 따라 요청 URL과 매칭되는 핸들러를 찾는 역할   

  0. @Controller, @RequestMapping 어노테이션이 붙은 핸들러
  1. 스프링 빈 이름의 핸들러

<br>


# Handler Adapter
- 찾은 핸들러를 실행시키는 역할  

  0. 어노테이션 기반의 핸들러
  1. HttpRequestHandler 인터페이스를 통해 구현된 핸들러
  2. Controller 인터페이스를 통해 구현된 핸들러

<br>


# View Resolver
- 핸들러가 반환한 ModelAndView를 알맞은 View로 전달하기 위해 View 생성
- 문자열 형태의 View 이름 반환
    - "home" → "home.html", "home.jsp"
- 다양한 View 템플릿 엔진
    - JSP, Thymeleaf 등