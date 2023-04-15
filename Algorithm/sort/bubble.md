# 버블 정렬 (Bubble Sort)
- 서로 인접한 2개의 원소끼리 자리를 교환하며 정렬하는 알고리즘
- 뒤에서부터 정렬 됨.

<br>

## 특징
  - 안정 정렬
  - 제자리 정렬
  - 맨 뒤에서부터 원소가 1개씩 정렬되어, 1회전을 수행할 때마다 정렬에서 제외되는 데이터가 하나씩 늘어난다.

<br>

## 구현 코드
```
public class Bubble {
    public static void main(String[] args) {
        int[] arr = {3, 1, 9, 5, 7};

        for (int i = arr.length-1; i > 0; i--) { // 1회전 마다 반복 값이 줄어듦
            for (int j = 0; j < i; j++) {
                if (arr[j] > arr[j+1]) {
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }

        for (int n : arr) {
            System.out.printf("%d ", n);
        }
    }
}
```