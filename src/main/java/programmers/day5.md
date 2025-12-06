# [요격 시스템](https://school.programmers.co.kr/learn/courses/30/lessons/181188)

## solution 

```java
import java.util.*;

class Solution {
    public int solution(int[][] targets) {
        int answer = 1;
        Arrays.sort(targets, (a,b) -> a[0]-b[0]);
        int prev = targets[0][1];
        for(int i=0; i<targets.length; i++){
            if(targets[i][0] >= prev) {
                answer++;
                prev = targets[i][1];
            }
        }
        return answer;
    }
}
```