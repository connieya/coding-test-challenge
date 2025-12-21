# [프로그래머스 -양궁대회](https://school.programmers.co.kr/learn/courses/30/lessons/92342?language=java)

## solution

```java
import java.util.*;

class Solution {
    private int[] answer;
    private int mx;

    private int compareScore(int[] ryan, int[] appeach) {
        int ret = 0;
        for (int i = 0; i < 11; i++) {
            if (ryan[i] == 0 && appeach[i] == 0) continue;
            if (ryan[i] > appeach[i]) ret += (10 - i);
            else ret -= (10 - i);
        }
        return ret;
    }

    private void dfs(int pos, int left, int[] ryan, int[] appeach) {
        if (pos < 0 && left > 0) return;

        if (left == 0) {
            int res = compareScore(ryan, appeach);
            if (res > mx) {
                mx = res;
                answer = ryan.clone();
            }
            return;
        }

        for (int i = left; i >= 0; i--) {
            ryan[pos] = i;
            dfs(pos - 1, left - i, ryan, appeach);
            ryan[pos] = 0;
        }
    }

    public int[] solution(int n, int[] info) {
        int[] ryan = new int[11];
        answer = new int[]{-1};
        mx = 0;

        dfs(10, n, ryan, info);
        return answer;
    }
}
```
