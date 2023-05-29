# Garbage Collection (가비지 컬렉션)
Java의 Heap 영역에서 동적으로 할당했던 메모리 중 더 이상 참조되지 않는 메모리를 주기적으로 삭제하는 프로세스

<br>

- 개발자가 수동으로 메모리 할당과 해제를 할 필요 없음
- 언제 GC가 발생하는 지 정확히 알 수 없음
- GC가 동작하는 동안은 다른 동작이 멈추기 때문에 오버헤드 발생 

<br>

# Young 영역
- 새로 생성된 객체가 할당되는 영역
- 많은 객체가 Young 영역에서 생성되었다가 사라진다
- Young 영역의 GC를 **Minor GC**라고 한다

<br><br>


# Old 영역
- Young 영역에서 살아남은 객체가 복사되는 영역
- Young 영역보다 크게 할당되며, Garbage가 적게 발생한다
- Old 영역의 GC를 **Major GC** 라고 한다

<br>


> ## Old 영역이 Young 영역보다 크게 할당되는 이유
> Young 영역의 수명이 짧은 객체들은 큰 공간이 필요 없고, 큰 객체들은 바로 Old 영역에 할당되기 때문

> ## 카드 테이블 (Card Table)
> Old 영역의 객체가 Young 영역의 객체를 참조할 때 그에 대한 정보 표시
> - Young 영역에서 GC가 실행될 때 Old 영역의 모든 객체를 식별할 필요 없이 카드 테이블만 조회해 GC의 대상인지 식별할 수 있음

<br><br>


# GC의 동작 방식
1. Stop The World
    - JVM이 애플리케이션의 실행을 멈춤
   - **GC를 실행하는 스레드를 제외한 모든 스레드의 작업이 중단**
2. Mark and Sweep
    - Mark : 사용되는 메모리와 사용되지 않는 **메모리 식별**
    - Sweep : Mark 단계에서 사용되지 않음으로 **식별된 메모리를 해체**

<br><br>


# Minor GC
## Young 영역의 구조
1개의 Eden 영역 + 2개의 Survivor 영역
- Eden 영역 : 새로 생성된 객체가 할당
- Survivor 영역 : 최소 1번의 GC 이상 살아남은 객체가 존재

<br>

>Eden 영역이 차면 **Minor GC**가 발생해, 사용되지 않는 메모리는 해체되고 사용중인 객체는 Survivor 영역으로 옮겨진다. **Survivor 영역은 반드시 1개의 영역에만 데이터가 존재**해야 한다.

<br>


## 동작 단계
1. 새로 생성된 객체가 Eden 영역에 할당
2. 객체가 계속 생성되어 Eden 영역이 가득 차고 Minor GC 실행  
    1) Eden 영역에서 사용되지 않는 객체의 메모리 해제
    2) Eden 영역에서 살아남은 객체는 1개의 Survivor 영역으로 이동
3. 1~2번의 과정이 반복, Survivor 영역이 가득 차면 살아남은 객체를 다른 Survivor 영역으로 이동 (1개의 Survivor 영역은 반드시 빈 상태)
4. 모든 과정을 반복해 계속 살아남은 객체는 Old 영역으로 이동 

- 객체의 생존 횟수 카운트를 위해 Minor GC에서 객체가 살아남은 횟수를 의미하는 age를 Object Header에 기록
- Minor GC 할 때 Object Header에 기록된 age를 보고 Old 영역으로 이동 여부 결정
- Survivor 영역 중 1개는 반드시 사용되어야 함. 2개의 영역 모두에 데이터가 존재하거나, 모두 사용량이 0이라면 현재 시스템이 비정상적임을 파악할 수 있음

<br><br>


# Major GC
- 객체들이 계속 이동되어 Old 영역의 메모리가 부족해지면 발생
- Old 영역은 Young 영역보다 크고, Young 영역을 참조할 수도 있어 Major GC는 Minor GC의 10배 이상의 시간 소요
- Full Scan : Young 영역과 Old 영역을 동시 처리

<br><br>


> ## 요약
> GC는 Heap 영역에서 더이상 참조되지 않는 객체를 찾아 메모리를 해제하는 기능이다.  
**Young 영역과 Old 영역**으로 나뉘어진다. 객체가 새로 생성되면 Young영역의 Eden 영역에 할당 되고, Eden 영역이 가득 찰 경우 **Minor GC**가 발생해 사용되지 않는 객체는 해제되고 살아남은 객체들은 Survivor 영역으로 옮겨진다. 이때 2개의 Survivor 영역 중 1군데는 반드시 비어져있어야 하고, 1군데는 사용되어야 한다.  
Survivor 영역도 가득 찰 경우 Old 영역으로 이동된다. Old 영역이 차면 **Major GC**가 발생한다. 


<br>

### 참고 자료
https://mangkyu.tistory.com/118
https://coding-factory.tistory.com/829