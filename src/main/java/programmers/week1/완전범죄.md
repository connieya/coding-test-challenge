# [완전 범죄](https://school.programmers.co.kr/learn/courses/30/lessons/389480)

## Solution 

```java
import java.util.*;

class Solution {
    int len; 
    int answer = Integer.MAX_VALUE;
    Set<String> set = new HashSet<>();
    
    
    public void dfs(int sumA , int sumB , int depth , int[][]arr, int n , int m) {
        if(sumA >= n || sumB >= m || sumA >= answer) {
            return;
        }
        String str = sumA+","+sumB+","+depth;
      
    
        if(depth == len) {
            answer = Math.min(answer ,sumA);
            return;
        }
        
        if(set.contains(str)) {
            return;
        }
         set.add(str);
        
        
        dfs(sumA+arr[depth][0] , sumB , depth+1 , arr , n, m);
        dfs(sumA,sumB+arr[depth][1] , depth+1, arr, n,m);
    }
    
    
    public int solution(int[][] arr, int n, int m) {    
        len = arr.length;
        dfs(0,0,0,arr,n,m);
        
        return answer == Integer.MAX_VALUE ? -1 : answer;
    }
}
```
