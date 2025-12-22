# [달리기 경주](https://school.programmers.co.kr/learn/courses/30/lessons/178871)

## solution

```java
import java.util.*;

class Solution {
    public String[] solution(String[] players, String[] callings) {
        Map<String, Integer> mp = new HashMap<>();
        for(int i=0; i<players.length; i++) {
            mp.put(players[i] , i);
        }
        
        for(String calling : callings) {
            int rank = mp.get(calling);
            mp.put(calling, rank-1);
            mp.put(players[rank-1] , rank);
            
            String temp = players[rank-1];
            players[rank-1] = calling;
            players[rank] = temp;
        }
       
        return players;
    }
}
```

### 풀이

**알고리즘**

- 해시맵 (HashMap) + 시뮬레이션

**접근 방법**

- HashMap을 사용하여 선수 이름 → 등수(인덱스) 매핑을 저장
- 호출된 선수가 앞 선수를 추월할 때, HashMap과 players 배열을 동시에 업데이트
- O(1) 시간에 선수의 현재 등수를 찾을 수 있어 효율적

**풀이 과정:**

1. HashMap 초기화: 선수 이름을 키로, 현재 등수(인덱스)를 값으로 저장
2. 각 호출(calling)에 대해:
   - 호출된 선수의 현재 등수(`rank`)를 HashMap에서 조회
   - 호출된 선수의 등수를 `rank-1`로 업데이트
   - 앞 선수(players[rank-1])의 등수를 `rank`로 업데이트
   - players 배열에서 두 선수의 위치를 실제로 교환
3. 최종 players 배열 반환

**시간 복잡도**

- O(n + m) - n = players 길이 (초기화), m = callings 길이 (각 호출마다 O(1) 연산)

**공간 복잡도**

- O(n) - HashMap에 선수 이름과 등수 저장

