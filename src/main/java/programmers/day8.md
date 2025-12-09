# [광물 캐기](https://school.programmers.co.kr/learn/courses/30/lessons/172927)

## solution

```java
import java.util.*;

class Solution {
    public int solution(int[] picks, String[] minerals) {
        return dfs(picks ,0, minerals, 0);
    }
    
    public int dfs(int[] picks, int index, String[] minerals, int sum){
        if(index >= minerals.length || (picks[0] == 0 && picks[1] == 0 && picks[2] == 0 )) {
            return sum;
        }
        
        int answer = 99999999;
        
        if(picks[0] > 0){
            picks[0]--;
            int c = 0;
            for(int i=index; i<index+5; i++){
                if(i == minerals.length) break;
                c++;
            }
            answer = Math.min(answer, dfs(picks,index+5,minerals,sum+c ));
            picks[0]++;
        }
        
        if(picks[1] > 0) {
            picks[1]--;
            int c = 0;
             for(int i=index; i<index+5; i++){
                if(i == minerals.length) break;
                if(minerals[i].equals("diamond")) {
                    c+=5;
                }else {
                    c++;
                }
            }
            answer = Math.min(answer , dfs(picks, index+5, minerals, sum+c));
            picks[1]++;
        }
        
        if(picks[2] > 0) {
            picks[2]--;
            int c = 0;
             for(int i=index; i<index+5; i++){
                if(i == minerals.length) break;
                if(minerals[i].equals("diamond")) {
                    c+=25;
                }else if(minerals[i].equals("iron")) {
                    c+=5;
                }else{
                    c++;
                }
            }
            answer = Math.min(answer, dfs(picks, index+5, minerals, sum+c));
            picks[2]++;
        }
        return answer;
    }
}
```