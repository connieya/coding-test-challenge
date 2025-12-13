# [리코쳇 로봇](https://school.programmers.co.kr/learn/courses/30/lessons/169199)

## solution

```java
import java.util.*;


class Point {
    int x;
    int y;
    int len;

    Point(int x, int y, int len){
        this.x = x;
        this.y = y;
        this.len = len;
    }
}


class Solution {
    int dx[] = {-1,0,1,0};
    int dy[] = {0,1,0,-1};

    public int solution(String[] board) {
        Queue<Point> queue = new LinkedList<>();
        int n = board.length;
        int m = board[0].length();

        boolean visited[][] = new boolean[n][m];



        for( int i=0; i<board.length; i++) {
            for(int j=0; j<board[i].length(); j++) {
                if(board[i].charAt(j) == 'R') {
                    queue.add(new Point(i,j,0));
                    visited[i][j] = true;
                    break;
                }
            }
        }

        while(!queue.isEmpty()) {
            Point now = queue.poll();
            if(board[now.x].charAt(now.y) == 'G') return now.len;

            for(int i=0; i<4; i++){
                int nx = dx[i] + now.x;
                int ny = dy[i] + now.y;
                while(true) {
                    if(nx < 0 || nx >= n || ny < 0 || ny >= m || board[nx].charAt(ny) =='D') {

                        if(!visited[nx-dx[i]][ny-dy[i]]) {
                            queue.add(new Point(nx-dx[i],ny-dy[i], now.len+1));
                            visited[nx-dx[i]][ny-dy[i]] = true;
                        }

                        break;
                    }
                    nx += dx[i];
                    ny += dy[i];
                }
            }
        }



        return -1;
    }
}
```

### 풀이

**알고리즘**

- BFS (너비 우선 탐색) & 시뮬레이션 (Simulation)

**접근 방법**

- 최단 거리를 구하기 위해 Queue 자료구조를 사용
- boolean 배열로 이미 방문한 위치를 기록하여 중복 방문 방지
- 한 번의 이동은 장애물이나 벽에 부딪힐 때까지 미끄러지는 것을 의미

**풀이 과정:**

1. 시작 위치('R') 찾아서 Queue에 추가 및 방문 처리
2. BFS 탐색:
   - 현재 위치가 목표('G')이면 이동 횟수 반환
   - 4방향(상하좌우)으로 이동 가능한 위치 탐색
   - 각 방향으로 장애물이나 벽에 부딪힐 때까지 미끄러지며 이동
   - 부딪히기 직전 위치가 방문하지 않은 곳이면 Queue에 추가
3. Queue가 비어도 목표에 도달하지 못하면 -1 반환

**시간 복잡도**

- O(n × m) - 보드의 모든 칸을 최대 한 번씩 방문
