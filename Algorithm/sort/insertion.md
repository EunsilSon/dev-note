# 삽입 정렬(Insertion Sort)
두번째 원소부터 시작해 앞의 원소들과 비교해 원소의 위치를 찾아 삽입하는 알고리즘

<br>

## 특징
  - 안정 정렬
  - 제자리 정렬


<br>

## 구현 코드
```
public class Insertion {
    public static void main(String[] args) {
        int[] arr = {4, 2, 10, 26, 7, 1};

        for (int i = 1; i < arr.length; i++) {
            int target = arr[i];

            int j;
            for (j = i-1; j >= 0 && arr[j] > target; j--) { // 앞의 원소가 타겟보다 작으면 멈춤
                arr[j+1] = arr[j];
            }
            arr[j+1] = target;
        }

        for (int n : arr) {
            System.out.printf("%d ", n);
        }
    }
}
```