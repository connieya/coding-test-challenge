# [프로그래머스 -하노이의 탑](https://school.programmers.co.kr/learn/courses/30/lessons/12946)

## solution

```java
import java.util.*;

class Solution {
    List<int[]> answer = new ArrayList<>();
    
    public void func(int a, int b, int n) {
        if (n == 1) {
            answer.add(new int[]{a, b});
            return;
        }
        
        // 1단계: 위의 n-1개를 중간 기둥으로
        func(a, 6 - a - b, n - 1);
        
        // 2단계: 가장 큰 원판을 목적지로
        answer.add(new int[]{a, b});
        
        // 3단계: 중간 기둥의 n-1개를 목적지로
        func(6 - a - b, b, n - 1);
    }
    
    public int[][] solution(int n) {
        func(1, 3, n);
        return answer.toArray(new int[answer.size()][]);
    }
}
```
