[자료구조와 알고리즘을 함께 Java! - chapter06 비선형 구조(힙 트리)](https://github.com/bjpublic/javarithms) 를 참고하여 정리한 내용입니다.

# 힙 트리 (Heap Tree)
- 완전 이진 트리를 기본으로 하며, 트리에서 최솟값 또는 최댓값을 빠르게 구하기 위한 자료구조
- 노드 값의 대소 관계는 부모-자식 간에만 성립하고, 형제 노드는 상관 없음
- 루트 노드에 접근 시 항상 최솟값 또는 최댓값을 가져올 수 있음

<br>

# 종류
## 최소 힙 트리
부모가 자식의 값보다 항상 작은 값이며, 전체 노드의 값 중에 가장 작은 값

## 최대 힙 트리
부모가 자식의 값보다 항상 큰 값이며, 전체 노드의 값 중에 가장 큰 값

<br>

# 최소 힙 트리 구현
## 멤버 변수
```java
private int[] heap;
private int size;
private int pointer;
```

## 생성자
```java
MinHeapTree(int size) {
    this.size = size;
    this.heap = new int[size + 1];
    this.heap[0] = -1;
    this.pointer = 0;
}
```
자식 노드를 쉽게 구하기 위해 배열의 0번은 -1로 비운다.  
편의상 비운 0번을 채우기 위해 `size + 1`만큼 힙 배열을 만든다.

<br>

## 부모의 인덱스 가져오기
부모 인덱스 = 자식 인덱스 / 2
```java
public int getParentIndex(int index) {
    if (index < 1) {
        return -1;
    }
    return index / 2;
}
```

<br>

## 왼쪽 자식의 인덱스 가져오기
왼쪽 자식 인덱스 = 부모 인덱스 * 2
```java
public int getLeftChildIndex(int index) {
    if (index < 1) {
        return -1;
    }
    return 2 * index;
}
```

<br>

## 오른쪽 자식의 인덱스 가져오기
오른쪽 자식 인덱스 = (부모 인덱스 * 2) + 1  
(왼쪽 자식 인덱스에 +1 한 값)
```java
public int getRightChildIndex(int index) {
    if (index < 1) {
        return -1;
    }
    return (2 * index) + 1;
}
```

<br>

## 리프 노드 판별 (자식 노드의 유무)
```java
public boolean isLeafNode(int index) {
    return getLeftChildIndex(index) > size && getRightChildIndex(index) > size;
}
```
왼쪽/오른쪽 자식 노드의 인덱스 값이 heap의 크기보다 크다는 것은 존재하지 않는 다는 것이다.

<br>

## 최솟값 가져오기
```java
public int getRoot() {
    return heap[1];
}
```
heap의 루트 노드가 항상 최솟값이다.

<br>

## 스왑 메서드
```java
public void swap(int currentIndex, int parentIndex) {
    int temp;
    temp = heap[currentIndex];
    heap[currentIndex] = heap[parentIndex];
    heap[parentIndex] = temp;
}
```
삽입, 삭제 연산 시 2개의 노드의 위치를 서로 바꿔준다.

<br>

## 모든 노드 출력하기
```java
public void print() {
    for (int i = 1; i <= size; i++) {
        int parent = heap[i];
        int leftChild = 2 * i <= size ? heap[2 * i] : -1;
        int rightChild = (2 * i) + 1 <= size ? heap[(2 * i) + 1] : -1;

        if (leftChild > -1 && rightChild > -1) {
            System.out.printf("부모: %s, 왼쪽 자식: %s, 오른쪽 자식: %s\n", parent, leftChild, rightChild);
        } else if (leftChild > -1 && rightChild == -1) {
            System.out.printf("부모: %s, 왼쪽 자식: %s, 오른쪽 자식은 없습니다.\n", parent, leftChild);
        } else if (leftChild == -1 && rightChild > -1) {
            System.out.printf("부모: %s, 왼쪽 자식은 없습니다., 오른쪽 자식: %s\n", parent, rightChild);
        } else {
            System.out.printf("리프 노드: %s\n", parent);
        }
    }
}
```
루트 노드의 왼쪽, 오른쪽 자식 노드의 인덱스를 구하고 존재 유무를 확인 후 출력한다.

<br>

## 삽입
```java
public void insert(int value) {
    heap[++pointer] = value; // 마지막 노드로 삽입
    int currentIndex = pointer;

    while (heap[currentIndex] < heap[getParentIndex(currentIndex)]) {
        swap(currentIndex, getParentIndex(currentIndex));
        currentIndex = getParentIndex(currentIndex);
    }
}
```
1. `pointer`를 +1 늘린 자리(마지막 자리)에 새 노드를 삽입한다.
2. 현재 인덱스 `current`는 `pointer` 가 된다.
3. 현재 노드의 값보다 부모 노드의 값이 더 크다면 두 노드의 자리를 swap한다.
4. 현재 인덱스 `current`는 부모 노드의 인덱스가 된다.

<br>

## 삭제
```java
public int delete() {
    int result = getRoot();

    heap[1] = heap[size];
    heap[size] = -1;
    size--;

    if (size > 1) {
        rebuild(1);
    }
    return result;
}
```
루트 노드를 변수에 옮기고, 마지막 노드를 루트 노드로 옮긴 후 heap을 재구성하기 위한 함수를 호출한다.

<br>

## heap 재구성
```java
private void rebuild(int current) {
    // current index를 기준으로 양쪽 자식을 구한다.
    int leftChildIndex = getLeftChildIndex(current);
    int rightChildIndex = getRightChildIndex(current);

    if (isLeafNode(current)) {
        return;
    }

    // 왼쪽 자식만 존재하는 경우
    int swapIndex = current;
    if (rightChildIndex > size) {
        if (heap[leftChildIndex] < heap[current]) {
            swapIndex = leftChildIndex;
        }
    } else {
        // current index를 기준으로 자식들 중 작은 값을 구한다.
        if (heap[leftChildIndex] <= heap[rightChildIndex]) {
            swapIndex = leftChildIndex;
        } else {
            swapIndex = rightChildIndex;
        }
    }

    // current가 swap값보다 크면 자리를 바꾼다.
    if (heap[current]> heap[swapIndex]) {
        swap(current, swapIndex);
        rebuild(swapIndex);
    }
}
```
1. current index 인자를 기준으로 양쪽 자식을 구하고, 자식들 중 작은 값`swapIndex`을 구한다.
2. `cuurent` 보다 `swapIndex`가 더 작으면 두 노드의 자리를 swap한다.
3. 다시 rebuild 함수를 재귀호출한다.

<br>

> 최소 힙을 최대 힙으로 구현하려면 **대소 관계**를 변경하고, 노드 삽입 메서드에서 **노드의 인덱스가 1인 경우에 ArrayIndexOutOfBoundsException 주의**