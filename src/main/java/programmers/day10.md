# [프로그래머스 - 충돌위험 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/340211)

## solution 1

```java
import java.util.*;

class Solution {
    static int start[];
    static Map<String , Integer> map = new HashMap<>();
    static int second = 0;
    public int solution(int[][] points, int[][] routes) {
        int answer = 0;
        
        int n = routes.length;
        
        for(int i=0; i<n; i++) {
            start = points[routes[i][0]-1];
            second = 0;
            boolean flag = true;
            for(int j=1; j<routes[i].length; j++){
                if(flag ) {
                    String key = ""+second+"s"+start[0]+","+start[1];
                    map.put(key, map.getOrDefault(key,0) +1);
                }
                move(start, points[routes[i][j]-1]);
                flag = false;
            }
        }
        
        for(String key : map.keySet()) {
            if(map.get(key) > 1) answer++;
        }
        
        
        return answer;
    }
    
    public void move(int[] s , int[] e) {
        int x1 = s[0];
        int y1 = s[1];
        int x2 = e[0];
        int y2 = e[1];
        while(x1 != x2 || y1 != y2) {
            if(x1 != x2) {
                x1 += Integer.compare(x2, x1);
            }else if(y1 != y2) {
                y1 += Integer.compare(y2,y1);
            }
            second++;  
            String key = ""+second+"s"+x1+","+y1;
            map.put(key, map.getOrDefault(key,0) +1);
        }
        start = e.clone();
        
    }
}
```