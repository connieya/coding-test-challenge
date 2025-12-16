# [프로그래머스 - 시소 짝꿍](https://school.programmers.co.kr/learn/courses/30/lessons/152996)

## solution 

```java
import java.util.*;

class Solution {
  public long solution(int[] weights) {
    long answer = 0;
    Map<Integer, Integer> map = new HashMap<>();

    for (int w : weights) {
      // 같은 무게
      answer += map.getOrDefault(w, 0);

      // 2배 (1:2 비율)
      answer += map.getOrDefault(w * 2, 0);

      // 절반 (2:1 비율)
      if (w % 2 == 0) {
        answer += map.getOrDefault(w / 2, 0);
      }

      // 2:3 비율 (w*2/3, w*3/2)
      if ((w * 2) % 3 == 0) {
        answer += map.getOrDefault((w * 2) / 3, 0);
      }
      if ((w * 3) % 2 == 0) {
        answer += map.getOrDefault((w * 3) / 2, 0);
      }

      // 3:4 비율 (w*3/4, w*4/3)
      if ((w * 3) % 4 == 0) {
        answer += map.getOrDefault((w * 3) / 4, 0);
      }
      if ((w * 4) % 3 == 0) {
        answer += map.getOrDefault((w * 4) / 3, 0);
      }

      // 현재 무게를 맵에 추가
      map.put(w, map.getOrDefault(w, 0) + 1);
    }

    return answer;
  }
}
    
```
