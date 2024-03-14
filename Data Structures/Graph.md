# 그래프 Graph
정점과 간선으로 이루어진 자료구조

<br>

## 구성 요소
- 정점 (Node / Vertex): 그래프에서의 위치
- 간선 (Edge / Link / Branch): 위치간의 관계, 각 정점을 연결하는 선
- 인접 정점 (Adjacent Vertex): 간선에 의해 직접 연결된 정점

<br>

## 그래프 종류
- 무방향: 간선을 통해 양방향으로 이동
- 방향: 간선에 방향이 존재
- 가중치: 간선에 비용 또는 가중치가 할당
- 연결: 무방향 그래프에서 항상 경로가 존재
- 비연결: 무방향 그래프에서 경로가 존재하지 않음
- 순환: 경로의 시작 정점과 종료 정점이 동일
- 비순환: 순환이 없음

<br>

> 그래프의 구현
> - 인접 행렬
> - 인접 리스트

> 그래프의 탐색
> - DFS(Depth First Search) 깊이 우선 탐색
> - BFS(Breadth First Search) 너비 우선 탐색

<br>

# 인접 리스트
ArrayList를 사용해 각 정점의 인접 리스트를 모두 갖게하는 방식

```java
public class AdjacencyList {
    private ArrayList<ArrayList<Integer>> listGraph;

    /**
     * 생성자
     * @param initSize
     */
    public AdjacencyList(int initSize) {
        this.listGraph = new ArrayList<ArrayList<Integer>>();
        for (int i = 0; i < initSize + 1; i++) { // ArrayIndexOutOfBoundsException 방지를 위해 초기 사이즈 +1 만큼 생성
            listGraph.add(new ArrayList<Integer>());
        }
    }

    public ArrayList<ArrayList<Integer>> getGraph() {
        return this.listGraph;
    }

    /**
     * 정점 반환
     * @param i
     * @return
     */
    public ArrayList<Integer> getNode(int i) {
        return this.listGraph.get(i);
    }

    /**
     * 그래프 추가 (양방향)
     * @param x
     * @param y
     */
    public void put(int x, int y) {
        listGraph.get(x).add(y);
        listGraph.get(y).add(x);
    }

    /**
     * 그래프 추가 (단방향)
     * @param x
     * @param y
     */
    public void putSingle(int x, int y) {
        listGraph.get(x).add(y);
    }

    /**
     * 인접리스트 출력
     */
    public void printAll() {
        for (int i = 1; i < listGraph.size(); i++) {
            System.out.printf("정점 %d의 인접 리스트", i);

            for (int j = 0; j < listGraph.get(i).size(); j++) {
                System.out.printf(" -> %d", listGraph.get(i).get(j));
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int initSize = 6;
        AdjacencyList adjacencyList = new AdjacencyList(initSize);

        adjacencyList.put(1, 2);
        adjacencyList.put(1, 3);
        adjacencyList.put(2, 3);
        adjacencyList.put(2, 4);
        adjacencyList.put(3, 4);
        adjacencyList.put(3, 5);
        adjacencyList.put(4, 5);
        adjacencyList.put(4, 6);

        adjacencyList.printAll();
    }
}
```

<br>

# 인접 행렬
- NxN 행렬로 표현하며, graph[i][j] == true 라면 정점 i에서 정점 j로의 간선이 존재함을 의미함
- 정점의 개수가 V일 때, V^2 크기의 2차원 배열을 생성해 구성

```java
public class AdjacencyArray {
    private int[][] arrGraph;

    /**
     * 인접 행렬 생성자
     * @param initSize
     */
    public AdjacencyArray(int initSize) {
        this.arrGraph = new int[initSize+1][initSize+1];
    }

    /**
     * 그래프 반환
     * @return
     */
    public int[][] getGraph() {
        return this.arrGraph;
    }

    /**
     * 그래프 추가(양방향)
     * @param x
     * @param y
     */
    public void put(int x, int y) {
        arrGraph[x][y] = arrGraph[y][x] = 1;
    }

    /**
     * 그래프 추가 (양방향 가중치)
     *  간선이 존재하는 행렬에는 가중치 값을 설정
     * @param x
     * @param y
     * @param w
     */
    public void put(int x, int y, int w) {
        arrGraph[x][y] = arrGraph[y][x] = w;
    }

    /**
     * 그래프 추가(단방향)
     * @param x
     * @param y
     */
    public void putSingle(int x, int y) {
        arrGraph[x][y] = 1;
    }

    /**
     * 인접 행렬 출력
     */
    public void printAll() {
        for (int i = 0; i < getGraph().length; i++) {
            for (int j = 0; j < arrGraph[i].length; j++) {
                System.out.printf("%d ", arrGraph[i][j]);
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int initSize = 6;
        AdjacencyArray adjacencyArray = new AdjacencyArray(initSize);

        adjacencyArray.put(1, 2);
        adjacencyArray.put(1, 3);
        adjacencyArray.put(2, 3);
        adjacencyArray.put(2, 4);
        adjacencyArray.put(3, 4);
        adjacencyArray.put(3, 5);
        adjacencyArray.put(4, 5);
        adjacencyArray.put(4, 6);

        adjacencyArray.printAll();
    }
}
```

<br>

# 인접 리스트와 인접 행렬의 차이
- 인접 리스트
    - 리스트를 순차적으로 확인해 정점에 접근
    - 인접 노드를 쉽게 찾을 수 있음
    - 그래프에 **간선이 적게 존재하는 희소 그래프**

- 인접 행렬
    - 정점 v1,v2에 대해 한 번에 접근 가능
    - 인접 노드를 찾기 위해 모든 노드를 순회
    - 그래프에 **간선이 많이 존재하는 밀집 그래프**

<br>

## 참고 자료
[Java 인접행렬과 인접리스트를 이용하여 그래프 구현하기](https://freestrokes.tistory.com/87#comment13736643)
