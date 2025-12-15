# [미로 탈출](https://school.programmers.co.kr/learn/courses/30/lessons/159993)

## solution

```java
import java.util.*;

class Node {
    int x;
    int y;

    public Node(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Solution {
    int dx[] = {-1, 0, 1, 0};
    int dy[] = {0, 1, 0, -1};

    public int solution(String[] maps) {
        int n = maps.length;
        int m = maps[0].length();
        int leverX = 0, leverY = 0;
        int exitX = 0, exitY = 0;

        // 첫 번째 BFS: S -> L (레버까지의 거리)
        int[][] dist = new int[n][m];
        for (int i = 0; i < n; i++) {
            Arrays.fill(dist[i], -1);
        }

        Queue<Node> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (maps[i].charAt(j) == 'S') {
                    dist[i][j] = 0;
                    q.add(new Node(i, j));
                }
                if (maps[i].charAt(j) == 'L') {
                    leverX = i;
                    leverY = j;
                }
            }
        }

        while (!q.isEmpty()) {
            Node cur = q.poll();
            for (int i = 0; i < 4; i++) {
                int nx = cur.x + dx[i];
                int ny = cur.y + dy[i];
                if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
                if (dist[nx][ny] == -1 && maps[nx].charAt(ny) != 'X') {
                    dist[nx][ny] = dist[cur.x][cur.y] + 1;
                    q.add(new Node(nx, ny));
                }
            }
        }

        int res = dist[leverX][leverY];
        if (res == -1) return -1;

        // 두 번째 BFS: L -> E (레버에서 출구까지의 거리)
        for (int i = 0; i < n; i++) {
            Arrays.fill(dist[i], -1);
        }

        q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (maps[i].charAt(j) == 'L') {
                    dist[i][j] = 0;
                    q.add(new Node(i, j));
                }
                if (maps[i].charAt(j) == 'E') {
                    exitX = i;
                    exitY = j;
                }
            }
        }

        while (!q.isEmpty()) {
            Node cur = q.poll();
            for (int i = 0; i < 4; i++) {
                int nx = cur.x + dx[i];
                int ny = cur.y + dy[i];
                if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
                if (dist[nx][ny] == -1 && maps[nx].charAt(ny) != 'X') {
                    dist[nx][ny] = dist[cur.x][cur.y] + 1;
                    q.add(new Node(nx, ny));
                }
            }
        }

        if (dist[exitX][exitY] == -1) return -1;
        return dist[exitX][exitY] + res;
    }
}
```

### 풀이

**알고리즘**

- BFS (너비 우선 탐색)

**접근 방법**

- 시작점(S)에서 레버(L)까지, 레버에서 출구(E)까지 두 번의 BFS로 최단 거리 탐색
- 2차원 배열로 각 위치까지의 거리를 저장하며 방문 체크
- 4방향(상하좌우)으로 이동 가능한 통로만 탐색

**풀이 과정:**

1. 첫 번째 BFS: S -> L (레버까지의 거리)
   - 시작점(S)을 Queue에 추가하고 거리 0으로 초기화
   - 현재 위치에서 4방향으로 이동 가능한 위치 탐색
   - 벽('X')이 아니고 방문하지 않은 위치면 거리 갱신 후 Queue에 추가
   - 레버에 도달하지 못하면 -1 반환
2. 두 번째 BFS: L -> E (레버에서 출구까지의 거리)
   - 거리 배열을 초기화하고 레버(L)를 시작점으로 설정
   - 동일한 방식으로 BFS 탐색
   - 출구에 도달하지 못하면 -1 반환
3. 두 거리를 합쳐서 반환

**시간 복잡도**

- O(n × m) - 보드의 모든 칸을 최대 한 번씩 방문
