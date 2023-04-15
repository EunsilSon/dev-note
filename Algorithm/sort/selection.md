# 선택 정렬 (Selection Sort)
- 선택되어 있는 위치에 어떤 원소를 넣을지 선택하는 알고리즘
- 앞에서부터 차례대로 정렬

<br>

## 특징
  - 불안정 정렬
  - 제자리 정렬 (배열 내에서 교환하므로 추가적인 메모리가 필요 없음)

<br>

## 구현 코드
```
public class Selection {
    public static void main(String[] args) {
        int[] arr = {3, 1, 9, 5, 7};
        int minIndex, temp;

        for (int i = 0; i < arr.length; i++) {
            minIndex = i;
            for (int j = i+1; j < arr.length; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }
            // swap
            temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }

        for (int n : arr) {
            System.out.printf("%d ", n);
        }
    }
}
```