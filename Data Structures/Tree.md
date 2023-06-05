[자료구조와 알고리즘을 함께 Java! - chapter06 비선형 구조(트리)](https://github.com/bjpublic/javarithms) 를 참고하여 정리한 내용입니다.

<br>

# **트리** (Tree)
노드와 간선으로 이루어져 반복적으로 정의되는 계층적 비선형 자료구조

<br>

# 트리 순회
순회 방법은 전위(pre-order), 중위(in-order), 후위(post-order) 순회가 있다.  
루트를 방문하는 기점을 기준으로 생각하면 쉽다.

- 전위 순회: **루트** → 왼쪽 하위 → 오른쪽 하위
- 중위 순회: 왼쪽 하위 → **루트** → 오른쪽 하위
- 후위 순회: 왼쪽 하위 → 오른쪽 하위 → **루트**

![tree(1)](https://github.com/EunsilSon/coding-test-practice/assets/46162801/d3b67c0b-d252-400a-a4b3-ed6ed5aebba7)

위 트리 구조를 순회한다면  
- 전위: 1 - 2 - 4 - 5 - 3 - 6 - 7
- 중위: 4 - 2 - 5 - 1 - 6 - 3 - 7
- 후위: 4 - 5 - 2 - 6 - 7 - 3 - 1

<br>

# **트리** 구현 코드
```
public class Tree {

    class Node {
        Object data;
        Node left;
        Node right;

        public Node(Object data) {
            this.data = data;
            left = null;
            right = null;
        }

        /**
         * 왼쪽 자식 노드 연결
         * @param node
         */
        public void addLeft(Node node) {
            left = node;
        }

        /**
         * 오른쪽 자식 노드 연결
         * @param node
         */
        public void addRight(Node node) {
            right = node;
        }

        /**
         * 왼쪽 자식 노드 삭제
         */
        public void deleteLeft() {
            left = null;
        }

        /**
         * 오른쪽 자식 노드 삭제
         */
        public void deleteRight() {
            right = null;
        }
    }

    /**
     * 노드 생성
     * @param data
     * @return
     */
    public Node addNode(Object data) {
        Node n = new Node(data);
        return n;
    }
}
```
```
public static void main(String[] args) {
    Tree tree = new Tree();

    // 노드 생성
    Node node1 = tree.addNode(1);
    Node node2 = tree.addNode(2);
    Node node3 = tree.addNode(3);
    Node node4 = tree.addNode(4);
    Node node5 = tree.addNode(5);
    Node node6 = tree.addNode(6);
    Node node7 = tree.addNode(7);

    node1.addLeft(node2);
    node1.addRight(node3);
    node2.addLeft(node4);
    node2.addRight(node5);
    node3.addLeft(node6);
    node3.addRight(node7);
}
```
출처: [[자료구조, Java] 트리(Tree) 개념 정리 및 구현](https://readerr.tistory.com/35)

<br>

# **이진 트리** (Binary Tree)
트리의 종류 중 하나로, 모든 노드가 최대 2개의 자식 노드를 가지는 트리

<br>

# **완전 이진 트리** (Complete Binary Tree)
이진 트리의 특성을 가지면서, 마지막 레벨을 제외한 나머지 레벨들의 자식 노드가 2개인 트리
- 자식 노드 채우는 순서: 왼쪽 → 오른쪽

<br>

# 구현 방법
1. 배열
    - 마지막 레벨을 제외하고 모든 노드가 채워져있어 메모리 낭비 없이 배열로 구현 가능
    - 0번 인덱스는 편의상 비워둠 (-1로 표현)
2. 연결리스트

<br>

# 인덱스 기반으로 노드 구하는 규칙
- 왼쪽 자식 노드 : 2 X index (index <= 노드의 수)
- 오른쪽 자식 노드 : (2 X index) + 1 (index <= 노드의 수)
- 부모 노드 : 2 / index (index > 1)

<br>

# **완전 이진 트리** 구현 코드
```
public class BinaryTree {
    class Node {
        // '트리 구현 코드'의 Node 클래스와  동일하므로 생략
    }

    Node root;

    public void setRoot(Node node) {
        this.root = node;
    }

    public Node getRoot() {
        return this.root;
    }

    public void printAll(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            int leftNode = this.getLeftNode(arr, i);
            int rightNode = this.getRightNode(arr, i);

            if (leftNode > -1) {
                System.out.printf("%d의 왼쪽 자식 노드는 %d\n", arr[i], leftNode);
            }

            if (rightNode > -1) {
                System.out.printf("%d의 오른쪽 자식 노드는 %d\n", arr[i], rightNode);
            }
        }
    }

    private int getLeftNode(int[] arr, int index) {
        int findIndex = 2 * index;
        if (arr.length <= findIndex) {
            return -1;
        }

        return arr[findIndex];
    }

    private int getRightNode(int[] arr, int index) {
        int findIndex = (2 * index) + 1;
        if (arr.length <= findIndex) {
            return -1;
        }

        return arr[findIndex];
    }

    public static void main(String[] args) {
        BinaryTree binaryTree = new BinaryTree();
        int[] arr = {-1,9,7,15,4,8,11}; // 배열로 표현
        binaryTree.printAll(arr);
    }
}

```

<br>

# **이진 탐색 트리** (Binary Search Tree)
이진 트리를 활용해 데이터 탐색이 용이하도록 트리를 구성한 것

<br>

# 이진 탐색 트리의 전제조건
1. 노드 N을 기준으로 왼쪽 서브 트리 노드의 모든 키 값은 노드 N의 키 값보다 작아야 한다.
2. 오른쪽 서브 트리 노드의 키 값은 노드 N의 키 값 보다 커야 한다.
3. 같은 키의 값을 갖는 노드는 존재하지 않는다.
4. 왼쪽과 오른쪽 서브 트리도 이진 탐색 트리다.

<br>

# **검색** 구현 코드
```
public class BinarySearchTree {
    class Node {
        // '트리 구현 코드'의 Node 클래스와  동일하므로 생략
    }

    Node root;
    int size;

    public void setRoot(Node node) {
        this.root = node;
    }

    public Node getRoot() {
        return this.root;
    }

    /**
     * 노드 검색 (재귀)
     * @param node
     * @param value
     * @return
     */
    public boolean search(Node node, int value) {
        if (node == null) {
            return false;
        } else if (node.getValue() == value) {
            return true;
        } else if (node.getValue() > value) {
            return search(node.getLeft(), value);
        } else {
            return search(node.getRight(), value);
        }
    }

    /**
     * 노드 검색 (반복문)
     * @param value
     * @return
     */
    public Boolean search(int value) {

        if (this.root == null) {
            return false;
        }

        Node target = this.root;
        while (target != null) {
            if (target.value == value) {
                return true;
            } else if (target.getValue() > value) {
                target = target.getLeft();
            } else {
                target = target.getRight();
            }
        }
        return false;
    }
}
```
target 보다 찾는 값이 더 작으면 왼쪽 서브 트리로 이동, 찾는 값이 더 크면 오른쪽 서브 트리로 이동한다.

<br>

# **삽입** 구현 코드
```
public void insert(int value) {
        // 1. 루트가 null인 경우
        if (this.root == null) {
            this.root = new Node(value);
            return;
        }

        Node target = this.root;
        Node parent;

        while (target != null ){
            parent = target;

            if (target.getValue() == value) {
                System.out.println("값이 이미 존재합니다. 삽입을 중단합니다.");
                break;
            }

            // 2. 삽입할 값이 루트보다 작은 경우
            if (target.getValue() > value) {
                target = target.getLeft();

                if (target == null) {
                    parent.setLeft(new Node(value));
                }
            }

            // 3. 삽입할 값이 루트보다 큰 경우
            else {
                target = target.getRight();

                if (target == null) {
                    parent.setRight(new Node(value));
                }
            }
        }
    }ㅡㅡ 
```
1~3개의 전제조건을 지켜 새 노드를 삽입한다.  
삽입 할 값이 루트보다 작으면 왼쪽으로 이동하고, 루트보다 크면 오른쪽으로 이동한다. 왼쪽/오른쪽 노드가 null인 곳을 찾으면 새 노드를 삽입한다.

<br>

# **삭제** 구현 코드
**1. 자식 노드가 없는 노드**  
>    1. 삭제할 노드를 찾고, 자식 노드의 존재 여부 파악  
>    2. 리프 노드이므로, 해당 노드를 null로 초기화

**2. 자식 노드가 1개만 존재하는 노드**
>    1. 삭제할 노드를 찾고, 자식 노드의 존재 여부 파악  
>    2. 삭제할 노드의 부모 노드를 기억하고 해당 노드를 null로 초기화  
>    3. 삭제된 노드의 왼쪽 자식을 (2)에서 기억한 부모 노드의 자식 노드로 연결

**3. 자식 노드가 2개 존재하는 노드**
>    1. 삭제할 노드를 찾고, 자식 노드의 존재 여부 파악  
>    2. 삭제 노드와 대체할 노드(오른쪽 서브 트리의 왼쪽 리프 노드) 찾기  
>    3. 해당 노드를 null로 초기화하고, 삭제한 노드의 위치에 대체 노드로 재배치

<br>

```
/**
* 인자 node를 기준으로 오른쪽 서브트리의 리프 노드 구하기
* @param node
* @return
*/
public Node getMinimumNode(Node node) {
    if (node == null) {
        return null;
    }

    if (node.getLeft() != null) {
        return getMinimumNode(node.getLeft());
    }

    return node;
}
```
```
public Node delete (Node root, int value) {
    if (root == null) {
        return null;
    }

    if (root.getValue() == value) {
        // 1. 자식 노드가 모두 없는 경우
        if (root.getLeft() == null && root.getRight() == null) {
            root = null;
            return null;
        }
        
        // 2.1 왼쪽 자식 노드만 존재하는 경우
        else if (root.getLeft() != null && root.getRight() == null) {
            Node left = root.getLeft();
            root = null;
            return left;
        }
        
        // 2.2 오른쪽 자식 노드만 존재하는 경우
        else if (root.getLeft() == null && root.getRight() != null) {
            Node right = root.getRight();
            root = null;
            return right;
        }
        
        // 3. 자식 노드가 2개인 경우
        else {
            Node children = getMinimumNode(root.getRight()); // 오른쪽 서브트리의 리프 노드
            root.setValue(children.getValue());
            root.setRight(delete(root.getRight(), children.getValue())); // 오른쪽 서브트리의 리프 노드 삭제
        }
    }

    // 삭제할 값이 더 작으면 왼쪽 서브트리, 더 크면 오른쪽 서브트리
    if (root.getValue() > value) {
        root.setLeft(delete(root.getLeft(), value));
    } else {
        root.setRight(delete(root.getRight(), value));
    }

    return root;
    }
```