# Big-O 표기법
**알고리즘 성능**을 수학적으로 표기해주는 표기법으로, 불필요한 연산을 제거하여 알고리즘 분석을 쉽게 할 목적으로 사용된다.

<br>

- 시간 복잡도: 입력되는 n의 크기에 따라 실행되는 명령문의 실행 빈도수
- 공간 복잡도: 알고리즘이 실행될 때 사용하는 메모리 양(메모리의 발전으로 중요도가 낮아짐)

<br>

>**O(1) < O(log n) < O(n) < O(n log n) < O(n2) < O(2n) < O(n!)**  
>오른쪽으로 갈 수록 시간 복잡도가 높음

<br><br>

시간 복잡도에서 중요하게 보는 것은 가장 큰 영향을 미치는 **n의 단위**이다.  
<br>

# O(1) : 상수 시간
입력 데이터의 크기에 상관 없이 한 단계만 수행

```java
public void bigO (n) {
    System.out.println("Hello World!");
}
```

<br>

# O(log n) : 로그 시간
실행 횟수가 연산마다 특정 요인에 의해 반틈씩 줄어듦
- 예) 이진 검색(binary search)

<br>

# O(n) : 선형 시간
- 입력 값 n만큼 수행
- 입력 값과 문제 해결 단계 횟수가 1:1 관계를 가짐

```java
public void bigO (n) {
    for (int i = 0; i < n; i++) {
        System.out.println("Hello World!");
	}
}
```

<br>

# O(n log n) : 선형로그형
N*(log2N)번만큼 수행

<br>

# O(n^2) : 2차 시간
- 입력 값 n^2만큼 수행
- 입력 값이 증가할수록 처리 시간이 제곱배로 증가

```java
public void bigO (n) {
    for (int i = 0; i < n; i++) {
        System.out.print("Hello ");
		for (int j = 0; j < n; j++) {
		    System.out.println("World!");
		}
	}
}
```

<br>

# O(C^n) : 지수 시간
주어진 상수값 C 의 n 제곱만큼 수행
- 예) 피보나치 수열

<br>

## 참고 자료

[알고리즘의 시간 복잡도와 Big-O 쉽게 이해하기](https://blog.chulgil.me/algorithm/amp/)

[[Algorithm] 시간 복잡도 / 빅오 표기법](https://velog.io/@hahan/Algorithm-%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84-%EB%B9%85%EC%98%A4-%ED%91%9C%EA%B8%B0%EB%B2%95)

[시간복잡도 Big-O(빅오)란?](https://ssdragon.tistory.com/m/100)
