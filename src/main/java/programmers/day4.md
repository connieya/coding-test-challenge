# [비밀 코드 해독](https://school.programmers.co.kr/learn/courses/30/lessons/388352)

## solution 

```java
class Solution {
    
    private int[][] queries;
    private int[] answer;
    private int result = 0;
    
    public int dfs(int depth ,int n, int arr[] ,int start) {
       if(depth == 5) {
           
           boolean flag = true;
           for(int i=0; i<queries.length; i++) {
               int res = count(arr , queries[i]);
               if(res != answer[i]) {
                   flag = false;
               }
           }
           if(flag) {
              return 1;
           }
           return 0;
       }
        int result = 0;
        
        for(int i=start; i<=n; i++) {
            arr[depth] = i;
           result += dfs(depth+1, n, arr , i+1);
        }
        
        return result;
        
        
    }
    
    public int solution(int n, int[][] q, int[] ans) {
        this.queries = q;
        this.answer = ans;
        
        int arr[] = new int[5];
        return dfs(0,n,arr,1);
        
    }
    
    private int count(int arr[] , int target[]){
        int count = 0;
        for(int i=0; i<5; i++) {
            for(int j=0; j<5; j++) {
                if(arr[i] == target[j]) {
                    count++;
                    break;
                }
            }
        }
        return count;
    }
}
```