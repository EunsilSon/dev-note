# 컬렉션 프레임워크 Collection Framework
다수의 데이터를 저장하는 자료구조와 데이터를 처리하는 알고리즘을 구조화한 **클래스의 집합**

- **List 〈E〉** 
  - 순서 있음
  - 중복 가능
  - Vector, ArrayList, LinkedList, Stack, Queue

<br>

- **Set 〈E〉**
  - 순서 없음
  - 중복 불가능
  - HashSet, TreeSet

<br>

- **Map 〈K, V〉**
  -  Collection 인터페이스를 상속받지 않고, 구조상의 차이로 별도로 정의됨
  - key-value 형태
  - key 중복 불가능, value 중복 가능
  - HashMap, TreeMap, Hashtable, Properties

<br><br><br>

# 컬렉션 클래스 Collection Class
컬렉션 프레임워크에 속하는 인터페이스를 **구현한 클래스**

<br><br>

# 1. List 인터페이스
## ArrayList 〈E〉 클래스
- 배열을 사용해 **인덱스**로 원소에 접근 가능
- 크기 변경 불가능
- 추가, 삭제 느림
- **검색 빠름**

<br>

## LinkedList 〈E〉 클래스
- 순차적으로 데이터 저장
- 저장된 원소들은 비순차적으로 분포되지만, 원소들 사이를 **링크**(이전/다음 원소를 가리킴)로 연결해 구성
- 단일, 이중 연결 리스트 구현 가능
- **추가, 삭제 빠름**
- 검색 느림

<br>

## Vector 〈E〉 클래스
- ArrayList와 동일 (배열, 순서, 중복)
- 원소의 개수에 따라 자동으로 크기 조절
- thread-safe (멀티스레드 환경)

<br>

## Stack 〈E〉 클래스
- Vector 클래스를 상속받음
- 후입선출 Last In First Out

<br>

## Queue 〈E〉 인터페이스
- 선입선출 First In First Out

<br><br><br>

# 2. Set 인터페이스
- Set 인터페이스를 구현한 모든 Set 컬렉션 클래스는 
1. 저장 순서를 유지하지 않는다.
2. 중복 저장이 불가능하다.

<br>

## HashSet 〈E〉 클래스
- **해시 알고리즘** 사용으로 **검색**이 매우 빠름
  - 해시 알고리즘: 해시 함수를 사용해 데이터를 해시 테이블에 저장하고, 그것을 다시 검색하는 알고리즘
- LinkedHashSet : 저장 순서 유지

<br>

## TreeSet 〈E〉 클래스
- **데이터가 정렬된 상태**로 저장되는 **이진 검색 트리의 형태**로 원소 저장

<br><br><br>

# 3. Map 인터페이스
- Map 인터페이스를 구현한 모든 Map 컬렉션 클래스는 
1. key-valuse 방식 사용
2. 저장 순서를 유지하지 않는다.
3. Key 중복 불가능, Value 중복 가능

<br>


## HashMap 〈K, V〉 클래스
- 해시 알고리즘을 사용해 **검색 속도 빠름**
- key null값 가능
- 입력 순서 보장

<br>

## Hashtable 〈K, V〉 클래스
- thread-safe
- key null값 불가능
- Hashtable보다 HashMap을 사용하는 것이 좋음

<br>

## TreeMap 〈K, V〉 클래스
- **데이터가 정렬된 상태**(오름차순)로 저장되는 **이진 검색 트리의 형태**로 원소 저장
- 정렬 후 저장하기 때문에 HashMap보다 속도 느림

<br><br>

# 4. Iterator 〈K〉 인터페이스
- iterator() 메서드를 정의해 **원소에 접근**

<br>

### 사용하는 이유
컬렉션에 **저장된 데이터를 읽어오는 방법을 표준화**했기 때문에 코드 재활용이 가능하다.


<br>

## Enumeration 〈E〉 인터페이스
Java 초창기에 만들어진 인터페이스이며, Iterator과 동일하게 데이터를 읽어온다.

<br>

> Iterator와 Enumeration의 차이점<br>
- **스냅샷**
  - 객체를 순차 조회하기 전의 상태를 사진처럼 찍어 놓고, 변경 사항을 반영하지 않는 것으로, 조회 도중에 객체가 변경되어도 괜찮지만 스냅샷 간의 불일치 문제가 발생한다.
  - Iterator는 모든 데이터를 순차 조회하기 전에 변경 사항이 생기면 예외를 발생시켜 조회를 중지한다.

<br><br>

## ListIterator 〈E〉 인터페이스
- 데이터 추가, 조회 작업 시 양방향으로 이동

<br><br>

# 5. Comparable과 Comparator
## Comparable〈T〉 인터페이스
- compareTo(T o) 메서드를 재정의해 원하는 기준으로**객체 정렬**(default: 오름차순)
- 자기 자신과 매개변수와 값을 비교
- java.lang package (import 불필요)

<br>

## Comparator〈T〉 인터페이스
- compare(T o, T o) 메서드 재정의
- 매개변수의 두 객체를 서로 비교
- java.util package (import 필요)
