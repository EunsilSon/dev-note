# String
- 불변(immutable) 객체
- 값 수정할 때 마다 새 메모리 영역 생성
- String Pool에서 따로 관리
- 문자열 리터럴을 바로 입력할 경우, String Pool에서 같은 문자열끼리 객체를 공유해 메모리가 절약됨
![String](https://user-images.githubusercontent.com/46162801/234633593-f0369339-1953-4664-920f-2c459d83444e.JPG)

- 클라이언트와 통신할 때 외부에서 데이터가 변경되는 것을 예방해 보안적

<br>

>### Java의 String이 불변 객체이기에 얻는 이점
> 1. 클라이언트와 문자열로 데이터를 통신할 때 외부에서 데이터가 변경되는 것을 예방할 수 있다.
> 2. 멀티스레드 환경에서 안전하고 값 변경이 없으니 동기화 문제에서 자유롭다.
> 3. String 전용 메모리 영역인 String Pool에서 따로 관리하여 메모리 절약이 된다.

<br>

**문자열 추가, 수정, 삭제 연산이 빈번한 경우** Heap 메모리에 많은 임시 Garbage가 생성돼 **Heal 메모리가 부족해짐**

이를 해결하기 위해 **가변성을 가진 ```StringBuilder```와 ```StringBuffer``` 클래스** 도입

<br><br>

# StringBuilder
- 가변(mutable) 객체
- 싱글스레드 환경
- 비동기 → thread-safe 하지 않아 병렬 상황에서 안전하지 않음
- (싱글스레드 환경에서) 속도 빠름

<br><br>

# StringBuffer
- 가변 객체
- 멀티스레드 환경
- 동기 → thread-safe 해서 병렬 상황에서 안전함
- 속도 느림

<br><br>

# 상황 별 사용하기 좋은 클래스
```String``` : 문자열 연산이 적고, 멀티스레드  

```StringBuffer``` : 문자열 연산이 많고, 멀티스레드  

```StringBuilder``` : 문자열 연산이 많고, 싱글스레드 or 동기화를 필요로하지 않는 경우