# [퍼즐 게임 챌린지](https://school.programmers.co.kr/learn/courses/30/lessons/340212)

## solution 

```java
import java.util.*;

class Solution {
    public int solution(int[] diffs, int[] times, long limit) {
        int maxLevel = Arrays.stream(diffs).max().orElse(1);
        int minLevel = 1;
        
        int answer = -1;
        
      
        while(minLevel <= maxLevel) {
            int level = (minLevel + maxLevel) / 2;
            
            // 전체 시간 계산
            long totalTime = times[0];
            
            for(int i = 1; i < diffs.length; i++) {
                int diff = diffs[i];
                int timeCur = times[i];
                int timePrev = times[i - 1];
                
                if(level >= diff) {
                    totalTime += timeCur;
                } else {
                    totalTime += (long)(diff - level) * (timePrev + timeCur) + timeCur;
                }
                
               
                if(totalTime > limit) {
                    break;
                }
            }
            
            // ✅ limit와 비교!
            if(totalTime <= limit) {
                answer = level;
                maxLevel = level - 1;
            } else {
                minLevel = level + 1;
            }
        }
        
        return answer;
    }
}
```
