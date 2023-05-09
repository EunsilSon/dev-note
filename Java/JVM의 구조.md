# JVM(Java Virtual Machine)
자바 프로그램 실행 환경을 만들어주는 소프트웨어

<br>

> ## Java는 플랫폼에 비종속적이고, JVM은 플랫폼에 종속적이다.
> 자바 언어로 된 .java파일을 컴파일하면 바이트코드로 된 .class 파일이 생성된다.
>
> Java는 컴파일된 바이트코드로 어떤 JVM에서도 동작시킬 수 있어 플랫폼에 종속적이지 않다.  
> 반대로, JVM은 해당 플랫폼에 적합하도록 각각 다르게 구현되기 때문에 플랫폼에 종속적이다. (윈도우의 JVM과 리눅스의 JVM은 다르다)

<br><br>

# JVM의 작동 과정

1. 자바 컴파일러(javac)가 자바 소스코드(.java)를 자바 바이트코드(.class)로 컴파일한다.
2. Class Loader를 통해 JVM의 Runtime Data Area로 로딩한다.
3. Runtime Data Area에 로드된 .class는 실행 엔진을 통해 해석된다.
4. 해석된 바이트코드는 Runtime Data Area의 각 영역에 배치돼 수행되고, 실행 엔진에 의해 GC의 작동과 스레드 동기화가 이루어진다.

<br>

## 클래스 로더 (Class Loader)
컴파일하여 생성된 .class파일을 Runtime Data Area의 Method Area로 적재

<br>

## 실행 엔진 (Execution Engine)
Method Area의 바이트코드를 실행 엔진에 제공해 바이트코드를 명령어 단위로 읽어 실행

<br>

## 가비지 컬렉터 (Garbage Collector)
- Heap Area에서 더 이상 참조되지 않는 객체를 탐색 후 제거
- GC를 수행하는 스레드를 제외한 나머지 모든 스레드는 일시정지 상태가 됨

<br><br>

# 런타임 데이터 영역 (Runtime Data Area)
JVM의 메모리 영역으로서 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역
![runtime_data_area](https://user-images.githubusercontent.com/46162801/237014890-13f84c20-7821-4a09-bfa5-48d85ee58e84.JPG)
출처: https://coding-factory.tistory.com/828

<br>

>### 모든 스레드가 **공유**하여 사용 (GC의 대상)
>- Heap Area
>- Method Area
>
>### 스레드마다 하나씩 생성
>- Stack Area
>- PC Register
>- Native Method Stack

<br><br>

## Method Area
- 클래스 멤버 변수(이름, 데이터 타입, 접근제어자) 관련, 메서드 정보
- Constant Pool, static, final class

<br>

## Heap Area
- new 생성자로 생성된 객체와 배열
- GC 활동 영역
  - 더 이상 참조되지 않는 객체 정리
  - 사용하지 않는 동적 메모리 블럭을 찾아 사용 가능한 자원으로 자동 회수

![heap_area](https://user-images.githubusercontent.com/46162801/237015545-eee56ba3-1b92-4e14-aefa-2d033afa4c89.JPG)
출처: https://coding-factory.tistory.com/828

힙 영역은 **GC**를 위해 3가지의 영역으로 나뉜다.

Young 영역
- 자바 객체가 생성되자마자 저장
- 객체 생성 후 최초로 Eden 영역에 할당되고, 데이터가 어느정도 쌓이면 Servivor의 빈 공간으로 이동 또는 회수

<br>

Old 영역
- Young(Eden+Survivor) 영역이 차게 되면 Old 영역으로 이동 또는 회수
- Old 영역이 차게 되면, Old 영역에 있는 모든 객체를 검사해 한 번에 삭제하는 GC가 실행됨. 이때 GC는 오래 걸리는 작업이므로 GC 스레드를 제외한 모든 스레드가 멈춤 **→ Stop-the-World **

<br>

> Young 영역의 GC → Minor GC  
> Old 영역의 GC → Major GC

<br>

## Stack Area
- 지역변수, 매개변수, 리턴 값, 연산에 사용되는 임시 값

<br>

## PC 레지스터
- 스레드 생성 시 생성됨
- 현재 스레드가 실행되는 부분의 주소와 명령 저장

<br>

## Native Method Stack
- Java 외의 언어로 작성된 코드를 위한 공간

<br><br>

> ## JDK와 JRE의 차이
> JDK(Java Development Kit)
> - Java를 사용하기 위해 필요한 모든 기능을 갖춘 Java용 SDK(Software Development Kit)
> - JDK는 JRE를 포함하고 있다.
> - 프로그램 생성, 실행, 컴파일 가능
>
> JRE(Java Runtime Environment)
> - JVM + 자바 클래스 라이브러리 등
> 컴파일 된 자바 프로그램을 실행하는데 필요한 패키지

<br>

> # 요약
> - JDK는 자바 프로그램을 실행, 컴파일을 위한 개발용 도구로서 JRE, JVM을 모두 갖고있는 포괄적인 키트   
> - JRE는 자바 프로그램을 실행할 수 있게 해주는 도구  
> - JDK > JRE > JVM

<br>

출처: https://doozi0316.tistory.com/entry/1%EC%A3%BC%EC%B0%A8-JVM%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B8%EA%B0%80