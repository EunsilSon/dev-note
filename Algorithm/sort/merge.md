# 합병 정렬 (Merge Sort)
- **분할 정복 알고리즘** 중 하나로, 배열을 균등한 크기로 분할할 수 없을 때까지 분할하고 두개의 부분 배열을 정렬과 동시에 병합하는 알고리즘

- **정렬과 병합을 함께 하는 것**을 **정복**이라고 한다.

<br>

## 특징
  - 추가적인 메모리 필요
  - 안정 정렬

<br>

## 구현 코드
```
import java.util.Arrays;

public class MergeSort {
    public static void main(String[] args) {
        MergeSort m = new MergeSort();
        int[] arr = {4, 2, 1, 7, 85, 34};
        m.merge(arr, 0, arr.length-1);
        System.out.println(Arrays.toString(arr));
    }

    /**
     * 분할
     */
    public void merge(int[] arr, int left, int right) {
        if (left < right) {
            int div = (left + right) / 2;

            merge(arr, left, div); // 왼쪽 배열
            merge(arr, div + 1, right); // 오른쪽 배열
            mergeSort(arr, left, div, right); // 정복 = 병합 + 정렬
        }
    }

    /**
     * 정복
     */
    public void mergeSort(int[] arr, int start, int div, int end) {
        int[] temp = new int[arr.length];
        int s = start;
        int r = div + 1;
        int k = start;

        // 정복
        while (s <= div && r <= end) {
            if (arr[s] <= arr[r]) {
                temp[k++] = arr[s++];
            } else {
                temp[k++] = arr[r++];
            }
        }

        while (s <= div) {
            temp[k++] = arr[s++];
        }

        while (r <= end) {
            temp[k++] = arr[r++];
        }

        for (int h = 0; h <= end - start; h++) {
            arr[start + h] = temp[start + h];
        }
    }
}
```