# CI/CD (Continuous Integration/Continuous Delivery)
- 애플리케이션 개발 단계를 자동화하여 사용자에게 빈번히 배포할 수 있는 것

<br><br>

# CI (지속적인 통합, Continuous Integration)
- 빌드/테스트 자동화
- 새로운 코드에 대한 변경사항이 자동으로 빌드 및 테스트

<br>

## CI가 필요한 환경
1. 여러 명의 개발자가 형상관리 툴을 공유해 사용
    - 소스코드의 충돌 방지
2. MSA 환경
    - 기능 별로 서비스를 잘게 쪼개어 개발하는 환경에서 기능 추가가 매우 빈번하게 발생함
    - 기능 충돌 방지

<br>


## CI의 핵심 목표
- 버그를 신속하게 찾아 해결
- 소프트웨어 품질 개선
- 새로운 업데이트의 검증 및 릴리즈 시간 단축 + 개발 편의성 증가

<br><br>


# CD (지속적인 서비스 제공 Continuous Delivery & 배포 Deployment)
- 배포 자동화
- CI를 통과한 코드를 자동으로 배포

<br>


## CD의 핵심 목표
- 개발자는 배포보다 개발에 집중 가능
- 수작업 없이 사용자에게 서비스 제공 가능

<br><br>

> ## 요약
> CI/CD는 빌드부터 배포까지의 과정을 자동화하는 것이다.  
CI는 지속적인 통합으로, 빌드와 테스트를 자동화한다. CD는 지속적인 서비스 제공과 배포로, CI를 거친 코드를 자동으로 배포한다. 자동화를 통해 개발자는 개발에 더 집중할 수 있고, 수작업으로 인한 실수를 줄여 빠르게 사용자에게 서비스를 제공할 수 있다.

<br>


### 참고 자료
https://seosh817.tistory.com/104
https://artist-developer.tistory.com/24
https://jud00.tistory.com/entry/CICD%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C