# [프로그래머스 - 과제 진행하기](https://school.programmers.co.kr/learn/courses/30/lessons/176962)

## solution

### 풀이

**알고리즘**

- 스택 (Stack) + 시뮬레이션

**접근 방법**

- 시작 시간 기준으로 정렬 후, 이전 과제와 현재 과제의 시간 관계를 확인
- 스택에 중단된 과제(인덱스, 남은 시간)를 저장하고, 여유 시간이 생기면 처리

**풀이 과정:**

1. 시작 시간 기준으로 정렬
2. 이전 과제 종료 시간과 현재 과제 시작 시간 비교
   - 정확히 끝나면: 완료 리스트에 추가
   - 여유 시간이 있으면: 완료 리스트에 추가 후, 스택의 중단된 과제 처리 (여유 시간만큼)
   - 시간이 부족하면: 남은 시간과 함께 스택에 저장
3. 마지막 과제 처리 후 스택의 모든 과제 처리 (LIFO 순서)

**시간 복잡도**

- O(n log n) - 정렬 시간

```java
import java.util.*;

class Solution {

    public int convertTovalue(String time){
        return Integer.parseInt(time.split(":")[0]) * 60
            + Integer.parseInt(time.split(":")[1]);
    }

    public String[] solution(String[][] plans) {
        List<String> answer = new ArrayList<>();

        Stack<int[]> stack = new Stack<>();

        Arrays.sort(plans, (a, b) -> a[1].compareTo(b[1]));

        for(int i = 1; i < plans.length; i++){

            int startTime = convertTovalue(plans[i][1]);
            int playTime = Integer.parseInt(plans[i][2]);

            int prevStartTime = convertTovalue(plans[i-1][1]);
            int prevPlanTime = Integer.parseInt(plans[i-1][2]);

            if(prevStartTime+prevPlanTime == startTime){
                answer.add(plans[i-1][0]);
            }else if(prevStartTime+prevPlanTime < startTime){
                answer.add(plans[i-1][0]);
                int extraTime = startTime- (prevStartTime+prevPlanTime);
                while(!stack.isEmpty()) {
                    int prev [] = stack.peek();
                    if(extraTime >= prev[1]){
                        answer.add(plans[prev[0]][0]);
                        stack.pop();
                        extraTime -= prev[1];
                    }else {
                        stack.pop();
                        stack.add(new int[]{prev[0],prev[1]-extraTime});
                        break;
                    }
                }
            }else {
                stack.add(new int[]{i-1,prevPlanTime - (startTime-prevStartTime)});
            }

        }

        answer.add(plans[plans.length-1][0]);

        while(!stack.isEmpty()){
            int prev[] = stack.pop();
            answer.add(plans[prev[0]][0]);
        }

        return answer.stream().toArray(String[]::new);
    }
}
```
