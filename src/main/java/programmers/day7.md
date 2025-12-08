# [호텔 대실](https://school.programmers.co.kr/learn/courses/30/lessons/155651)

## solution 

```java
import java.util.*;

class Solution {

    private int toMinutes(String time) {
        String[] t = time.split(":");
        return Integer.parseInt(t[0]) * 60 + Integer.parseInt(t[1]);
    }

    public int solution(String[][] book_time) {
        // 1) 시작 시각 기준 정렬
        Arrays.sort(book_time, Comparator.comparing(t -> t[0]));

        PriorityQueue<Integer> pq = new PriorityQueue<>(); // 종료시각(분) 저장

        for (String[] time : book_time) {
            int start = toMinutes(time[0]);
            int end = toMinutes(time[1]);

            // 2) 가장 빨리 비는 방이 청소까지 끝났으면 재사용
            if (!pq.isEmpty() && pq.peek() + 10 <= start) {
                pq.poll();
            }
            // 3) 현재 예약을 방에 배정
            pq.offer(end);
        }

        // 4) 힙 크기가 필요한 최소 객실 수
        return pq.size();
    }
}
```