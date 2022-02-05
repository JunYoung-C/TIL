# 최단경로

- 가장 짧은 경로를 찾는 알고리즘이다. 길찾기 문제라고도 불린다.
- 그리디 알고리즘의 한 유형에 속하기도 한다.
- 코딩테스트에서 요구되는 알고리즘은 [다익스트라](#다익스트라-알고리즘)와 [플로이드 워셜](플로이드-워셜-알고리즘)이다.

## 다익스트라 알고리즘

- 그래프에서 여러개의 노드가 있을 때, 특정한 노드에서 출발하여 다른 노드로 가는 각각의 최단경로를 구해주는 알고리즘이다.
- 시간 복잡도 : O(ElogV) - E : 간선의 개수, V : 노드의 개수
    - 우선순위 큐 사용 : 하나의 데이터를 삽입 및 삭제할 때의 시간 복잡도는 O(logN)
    - ElogE -(중복간선이 없다면 E는 항상 V^2이하)-> ElogV

### 코드

```java
class Node implements Comparable<Node> {
    int index;
    int cost;

    @Override
    public int compareTo(Node o) {
        return this.cost - o.cost;
    }
}

public class Main {
    public int[] solution(int n, int m, ArrayList<ArrayList<Node>> graph) {
        int[] answer = new int[n + 1]; // 최단거리 저장
        Arrays.fill(answer, Integer.MAX_VALUE);
        Priority<Node> pQ = new PriorityQueue<>();
        pQ.offer(new Node(1, 0));

        while (!pQ.isEmpty()) {
            Node now = pQ.poll();

            if (answer[now.index] < now.cost) {
                continue;
            }

            for (Node next : graph.get(now.index)) {
                if (answer[next.index] > now.cost + next.cost) {
                    answer[next.index] = now.cost + next.cost;
                    pQ.offer(new Node(next.index, answer[next.index]));
                }
            }
        }

        return answer;
    }

    public static void main(String[] args) {
        Main T = new Main();
        Scanner stdIn = new Scanner(System.in);

        ArrayList<ArrayList<Node>> graph = new ArrayList<>();
        int n = stdIn.nextInt(); // 노드의 개수
        int m = stdIn.nextInt(); // 간선의 개수

        for (int i = 0; i <= n; i++) {
            int a = stdIn.nextInt();
            int b = stdIn.nextInt();
            int c = stdIn.nextInt();
            graph.get(a).add(new Node(b, c));
        }

        int[] dis = T.solution(n, m, graph);
        for (int i = 2; i <= n; i++) {
            if (dis[i] == Integer.MAX_VALUE) {
                System.out.println(i + " : " + "impossible");
            } else {
                System.out.println(i + " : " + dis[i]);
            }
        }
    }
}
```

## 플로이드 워셜 알고리즘
- 다익스트라 알고리즘은 한 지점에서 다른 특정 지점까지의 최단 경로를 구해야 하는 경우에 사용한다.
- 플로이드 워셜 알고리즘은 모든 지점에서 다른 모든지점까지의 최단 경로를 모두 구해야하는 경우에 사용할 수 있는 알고리즘이다.
- 시간 복잡도 : O(N^3)
### 코드

```java
public class Main {
  public int[] solution(int n, int m, int[][] graph) {
      for (int k = 1; k <= n; k++) {
          for (int a = 1; a <= n; a++) {
              for (int b = 1; b <= n; b++) {
                  graph[a][b] = Math.min(graph[a][b], graph[a][k] + graph[k][b]);
              }
          }
      }
  }
    public static void Main(String[] args) {
        Main T = new Main();
        Scanner stdIn = new Scanner(System.in);

        int n = stdIn.nextInt(); // 노드의 개수
        int m = stdIn.nextInt(); // 간선의 개수

        int[][] graph = new int[n + 1][n + 1];
        for (int i = 0; i <= n; i++) {
            Arrays.fill(graph[i], Integer.MAX_VALUE);
        }
        // 자기자신에서 자기자신으로 가는 비용은 0으로 초기화
        for (int a = 1; a <= n; a++) {
            for (int b = 1; b <= n; b++) {
                if (a == b) {
                    graph[a][b] = 0;
                }
            }
        }

        for (int i = 0; i < m; i++) {
            int a = stdIn.nextInt();
            int b = stdIn.nextInt();
            int c = stdIn.nextInt();
            graph[a][b] = c;
        }

        T.solution(n, m, graph);

        for (int a = 1; a <= n; a++) {
            for (int b = 1; b <= n; b++) {
                if (graph[a][b] == Integer.MAX_VALUE) {
                    System.out.print("INFINITY");
                } else {
                    System.out.print(graph[a][b]);
                }
            }
            System.out.println();
        }
    }
}
```