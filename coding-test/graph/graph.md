# 다양한 그래프 알고리즘

- dfs/bfs와 최단경로 알고리즘은 그래프 알고리즘의 한 유형으로 볼 수 있다.
- 유니온-파인드, 크루스칼, 위상정렬 알고리즘 등이 있다.
- 그래프의 구현 방법
    - 인접 행렬 : 2차원 배열을 사용하는 방식. O(V^2)의 메모리공간 필요. a -> b의 임의의 간선을 O(1)의 시간으로 알 수 있음.
    - 인접 리스트 : 리스트를 사용하는 방식. O(E)의 메모리 공간 필요. a -> b의 임의의 간선을 O(V)의 시간으로 알 수 있음.

**그래프 vs 트리**

|     |그래프|트리|
|-----|---|---|
| 방향성 |방향 그래프 혹은 무방향 방향 그래프 |방향 그래프|
|순환성|순환 빛 미순환|비순환|
|루트 노드 존재 여부|루트 노드가 없음|루트 노드가 존재|
|노드간 관계성|부모와 자식 관계 없음|부모와 자식 관계|
|모델의 종류|네트워크 모델|계층 모델|


## Index

1. [union-find](#서로소-집합disjoint-sets)
2. [서로소 집합을 활용한 사이클 판별](#서로소-집합을-활용한-사이클-판별)
3. [크루스칼 알고리즘](#크루스칼-알고리즘)
4. [프림 알고리즘](#프림-알고리즘)
5. [위상 정렬(Topology Sort)](#위상-정렬Topology-Sort)

## 서로소 집합
(Disjoint Sets)

- union-find라고 부르기도 한다.
- 알고리즘 원리
    1. union(합집합) 연산을 확인하여, 서로 연결된 두 노드를 A, B 확인한다.
        - A와 B의 루트 노드 A', B'를 각각 찾는다.
        - A'를 B'의 부노 모드로 설정한다.(B'가 A'를 가리키도록 한다.)
    2. 모든 union(합집합) 연산을 처리할 때까지 1번 과정을 반복한다.

### 코드

```java
public class Main {
    public int find(int x, int[] parent) {
        if (parend[x] == x) {
            return x;
        }
        return parent[x] = find(parent[x], parent);
    }

    void unite(int a, int b, int[] parent) {
        a = find(a, parent);
        b = find(b, parent);
        // 낮은 숫자가 부모로 가도록 조정
        if (a < b) {
            parent[b] = a;
        } else {
            parent[a] = b;
        }
    }

    public static void main(String[] args) {
        Main T = new Main();
        Scanner stdIn = new Scanner(System.in);
        int v = stdIn.nextInt();
        int e = stdIn.nextInt();
        int[] parent = new int[v + 1];
        for (int i = 1; i <= v; i++) {
            parent[i] = i;
        }

        for (int i = 0; i < m; i++) {
            int a = stdIn.nextInt();
            int b = stdIn.nextInt();
            unite(a, b);
        }

        // 각 원소가 속한 집합 출력하기
        System.out.print("각 원소가 속한 집합: ");
        for (int i = 1; i <= v; i++) {
            System.out.print(findParent(i) + " ");
        }
        System.out.println();

        // 부모 테이블 내용 출력하기
        System.out.print("부모 테이블: ");
        for (int i = 1; i <= v; i++) {
            System.out.print(parent[i] + " ");
        }
        System.out.println();
    }
}
```

## 서로소 집합을 활용한 사이클 판별

- 서로소 집합은 무방향 그래프 내에서의 사이클을 판별할 수 있다.
- 알고리즘 원리
    1. 각 간선을 확인하며 두 노드의 루트 노드를 확인한다.
        - 루트 노드가 서로 다르다면 두 노드에 대하여 union 연산 수행한다.
        - 루트 노드가 서로 같다면 사이클이 발생한 것이다.
    2. 그래프에 포함되어 있는 모든 간선에 대하여 1번 과정을 반복한다.

## 크루스칼 알고리즘

- 신장트리(spanning tree) : 하나의 그래프가 있을 때 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프
- 크루스칼 알고리즘 : 신장트리 중에서 최소 비용으로 만들 수 있는 신장트리를 찾는 알고리즘이다.
- 알고리즘 원리
    1. 간선 데이터를 비용에 따라 오름차순으로 정렬한다.
    2. 간선을 하나씩 확인하며 현재의 간선이 사이클을 발생시키는지 확인한다.
        - 사이클이 발생하지 않는 경우 최소 신장 트리에 포함시킨다.
        - 사이클이 발생하는 경우 최소 신장 트리에 포합시키지 않는다.
    3. 모든 간선에 대하여 2번의 과정을 반복한다.
- 시간 복잡도 : O(ElogE), 간선을 정렬하는 작업이 제일 오래걸린다.

### 코드

```java
class Edge implements Comparable<Edge> {
    int v1;
    int v2;
    int cost;

    Edge(int v1, int v2, int cost) {
        this.v1 = v1;
        this.v2 = v2;
        this.cost = cost;
    }

    @Override
    public int compareTo(Edge ob) {
        return this.cost - ob.cost;
    }
}

public class Main() {
    public int find(int x, int[] parent) {
        if (parend[x] == x) {
            return x;
        }
        return parent[x] = find(parent[x], parent);
    }

    void unite(int a, int b, int[] parent) {
        a = find(a, parent);
        b = find(b, parent);
        // 낮은 숫자가 부모로 가도록 조정
        if (a < b) {
            parent[b] = a;
        } else {
            parent[a] = b;
        }
    }

    public static void main(String[] args) {
        Main T = new Main();
        Scanner stdIn = new Scanner(System.in);
        int v = kb.nextInt();
        int e = kb.nextInt();
        int[] parent = new int[n + 1];
        for (int i = 1; i <= v; i++) {
            parent[i] = i;
        }

        ArrayList<Edge> edges = new ArrayList<>();
        for (int i = 0; i < e; i++) {
            int a = stdIn.nextInt();
            int b = sc.nextInt();
            int cost = sc.nextInt();
            edges.add(new Edge(a, b, cost));
        }

        int answer = 0;
        // 간선을 비용 순으로 정렬
        Collections.sort(edges);
        for (Edge edge : edges) {
            int fv1 = T.find(edge.v1, parent);
            int fv2 = T.find(edge.v2, parent);
            if (fv1 != fv2) {
                answer += edge.cost;
                unite(fa1, fb2, parent);
            }
        }
    }
}
```

## 프림 알고리즘

- 크루스칼 알고리즘과 마찬가지로 신장트리 중에서 최소 비용으로 만들 수 있는 신장트리를 찾는 알고리즘이다.
- 알고리즘 원리
    1. 모든 노드가 연결되어 있는 그래프에서 시작 노드를 우선순위 큐에 넣는다.
        - 우선순위 큐는 비용을 기준으로 오름차순 정렬되어있다.
    2. 우선순위 큐가 빌때 까지 다음의 과정을 반복한다.
        - 방문하지 않고 최소 비용을 가진 노드를 선택한다.
        - 해당 노드와 연결된 노드 중 방문하지 않은 노드를 큐에 넣는다.

### 코드

```java
class Edge implements Comparable<Edge> {
    int destination;
    int cost;

    Edge(int v, int cost) {
        this.v = v;
        this.cost = cost;
    }

    @Override
    public int compareTo(edge ob) {
        return this.cost - ob.cost;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);
        int n = stdIn.nextInt(); // 노드의 수
        int m = stdIn.nextInt(); // 간선의 수
        ArrayList<ArrayList<Edge>> graph = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<>());
        }

        boolean[] visited = new boolean[n + 1];
        for (int i = 0; i < m; i++) {
            int a = stdIn.nextInt();
            int b = stdIn.nextInt();
            int c = stdIn.nextInt();
            graph.get(a).add(new Edge(b, c));
            graph.get(b).add(new Edge(a, c));
        }

        int answer = 0;
        PriorityQueue<Edge> p0Q = new PriorityQueue<>();
        pQ.off(new Edge(1, 0));

        while (!pQ.isEmpty) {
            Edge edge = pQ.poll();
            if (!visited[edge.destination]) {
                visited[edge.destination] = true;
                answer += edge.cost;
                for (Edge nextEdge : graph.get(edge.destination)) {
                    if (!visited[nextEdge.destination]) {
                        pQ.offer(new Edge(nextEdge.destination, nextEdge.cost));
                    }
                }
            }
        }

        System.out.println(answer);
    }
}
```

## 위상 정렬(Topology Sort)
- 위상 정렬이란 방향 그래프의 모든 노드를 방향성에 거시르지 않도록 순서대로 나열하는 것이다.
- 시간 복잡도 : O(V + E)
### 코드
```java
public class Main {
    void topologySort(int v, int e, int[] indegree, ArrayList<ArrayList<Integer>> graph) {
        ArrayList<Integer> result = new ArrayList<>(); // 알고리즘 수행 결과를 담을 리스트
        Queue<Integer> que = new LinkedList<>();
        
        // 진입차수가 0인 노드를 큐에 삽입
        for (int i = 1; i <= v; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
            }
        }
        
        while (!que.isEmpty) {
           int now = que.poll();
           result.add(now);
           for (int next : graph.get(now)) {
               indegree[next] -= 1;
               if (indegree[next] == 0) {
                   que.offer(next);
               }
           }
        }
        
        // 위상 정렬을 수행한 결과 출력
        for (int i = 0; i < result.size(); i++) {
            System.out.print(result.get(i) + " ");
        }
    }

    public static void main(String[] args) {
        Main T = new Main();
        Scanner stdIn = new Scanner(System.in);

        int v = stdIn.nextInt();
        int e = stdIn.nextInt();

        public static int[] indegree = new int[v + 1];
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<>());
        }


        for (int i = 0; i < e; i++) {
            int a = stdIn.nextInt();
            int b = stdIn.nextInt();
            graph.get(a).add(b); // a에서 b로 이동 가능
            indegree[b] += 1;
        }

        T.topologySort(v, e, indegree, graph);
    }
}
```