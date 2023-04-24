# 탐욕 알고리즘 (Greedy Algorithm)
현재에서 가장 최적인 해답을 도출하는 알고리즘

<br>

1. 선택
    * 탐욕적 선택 속성: 이후의 선택에 영향을 미치지 않는다.
    * 최적 부분 구조: 문제의 최종 해결 방법이 부분 문제에 대한 최적 문제 해결 방법과 동일하다.
2. 적절성 (문제 조건을 만족하는 지)
3. 해답 (문제가 해결 되었는 지)

<br>

**항상 최적의 결과는 보장하지 못한다**

<br>

## 대표적인 예시
거스름돈 문제: 가작 적은 동전의 개수 구하기
```
public class SmallCoinChange {
    public static void main(String[] args) {
        SmallCoinChange smallChange = new SmallCoinChange();
        System.out.println(smallChange.getSmallCoinChange(1260));
    }

    public int getSmallCoinChange(int change) {
        int coin = 0;

        coin += change / 500;
        change %= 500;
        coin += change / 100;
        change %= 100;
        coin += change / 50;
        change %= 50;
        coin += change / 10;

        return coin;
    }
}
```