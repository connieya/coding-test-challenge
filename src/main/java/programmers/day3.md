# [수식 최대화](https://school.programmers.co.kr/learn/courses/30/lessons/67257)

## solution 

```java
import java.util.*;

class Solution {
    
    boolean visited[];
    char []lookUp = {'+' , '-' , '*'};
    long ans = 0;
    List<Long> n1;
    List<Character> c1;
    
   private void dfs(int depth, List<Long> num, List<Character> ex, char ch[]) {
    if(depth == 3) {
        n1 = new ArrayList<>(num);
        c1 = new ArrayList<>(ex);
        
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < c1.size(); j++) {
                if(ch[i] == c1.get(j)) {
                    long result = solve(n1.get(j), n1.get(j+1), c1.get(j));
                    n1.remove(j+1);
                    n1.set(j, result);
                    c1.remove(j);
                    j--;
                }
            }
        }
        
        Long r = Math.abs(n1.get(0));
        if(r > ans) {
            ans = r;
        }
        
        return;  
    }
    
    for(int i = 0; i < 3; i++) {
        if(!visited[i]) {
            visited[i] = true;
            ch[depth] = lookUp[i];
            dfs(depth+1, num, ex, ch);
            visited[i] = false;
        }
    }
}
    
    public long solution(String expression) {
        List<Long> num = new ArrayList<>();
        List<Character> ex = new ArrayList<>();
        char ch[] = new char[3];
        visited = new boolean[3];
        
        String n = "";
        for(char c : expression.toCharArray()) {
            if(Character.isDigit(c)){
                n += c;
                continue;
            }
            ex.add(c);
            num.add(Long.parseLong(n));
            n = "";
        }
        num.add(Long.parseLong(n));
        
        
        char[]tmp = new char[3];
        
        dfs(0,num,ex,tmp);
        return ans;
    }
    
    private long solve(long a, long b , char ch) {
        if(ch == '*') return a*b;
        if(ch == '+') return a+b;
        return a-b;
    }
}
```
