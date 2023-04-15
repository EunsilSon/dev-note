# 퀵 정렬 (Quick Sort)
**분할 정복 알고리즘** 중 하나로, pivot을 기준으로 배열을 2개로 분할해 각각 정렬한 후 1개의 배열로 결합하는 알고리즘

<br>

## 특징
  - 불안정 정렬
  - 제자리 정렬
  - 이미 정렬된 배열에서는 오래 걸림

<br>

## 구현 코드
```
public class Quick {
    public static void main(String[] args) {
        int[] arr = new int[]{26, 10, 35, 19, 7, 3, 12};
        Quick quick = new Quick();
        quick.quickSortWithMiddlePivot(arr, 0, arr.length-1);

        for (int n : arr) {
            System.out.printf("%d ", n);
        }
    }

    public void quickSortWithMiddlePivot(int[] arr, int left, int right) {
        if (left >= right) {
            return;
        }

        int pivot = arr[(left + right) / 2];
        int i = left;
        int j = right;

        while (i < j) {
            while (arr[i] < pivot) {
                i++;
            }

            while (arr[j] > pivot) {
                j--;
            }

            if (i >= j) {
                break;
            }

            if (arr[i] == pivot && arr[j] == pivot) {
                i++;
            }

            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }

        quickSortWithMiddlePivot(arr, left, i-1);
        quickSortWithMiddlePivot(arr, i+1, right);
    }
}

```