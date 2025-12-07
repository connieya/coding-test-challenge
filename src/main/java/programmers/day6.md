# [바탕 화면 정리](http://school.programmers.co.kr/learn/courses/30/lessons/161990)

## solution 1

```java
import java.util.*;

class Solution {
    public int[] solution(String[] wallpaper) {
        int lux = Integer.MAX_VALUE;
        int luy = Integer.MAX_VALUE;
        int rdx = -1;
        int rdy = -1;
        for(int i=0; i<wallpaper.length; i++){
            for(int j=0; j<wallpaper[i].length(); j++) {
                if(wallpaper[i].charAt(j) == '#') {
                    lux = Math.min(lux,i);
                    luy = Math.min(luy,j);
                    rdx = Math.max(rdx,i+1);
                    rdy = Math.max(rdy,j+1);
                }
            }
        }
        
        int[] answer = {lux,luy,rdx,rdy};
        return answer;
    }
}
```