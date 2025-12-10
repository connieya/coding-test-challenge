# [프로그래머스 - 서버 증설 횟수](https://school.programmers.co.kr/learn/courses/30/lessons/389479)

## solution

```java
import java.util.*;

class Server {
    int time;
    int count;

    public Server(int time , int count) {
        this.time = time;
        this.count = count;
    }
}

class Solution {
    public int solution(int[] players, int m, int k) {
        // 서버 증설할 때의 시간 (인덱스) 와 증설 개수를 저장해야 할 듯
        int answer = 0;
        Queue<Server> queue = new LinkedList<>();

        for(int i=0; i<players.length; i++){
            int cnt = players[i];
            if(cnt / m > 0) { // 서버 증설 해야 함

                int needServers = cnt /m;
                while(!queue.isEmpty()) { // 기존에 증설한 서버 확인
                    Server s = queue.peek();
                    if(s.time+k-1 < i) { // 서버 운영 시간 지남
                        queue.poll();
                    }else { // 서버 운영 시간 아직 안 끝남
                        break;
                    }

                }
                int currentServers = 0;
                for(Server s : queue) {
                     currentServers += s.count;
                }

               int addServers = needServers - currentServers;
                if(addServers > 0) {
                    answer += addServers;
                    queue.add(new Server(i, addServers));
                }


            }
        }

        return answer;
    }
}
```
