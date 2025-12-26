# [메뉴 리뉴얼](https://school.programmers.co.kr/learn/courses/30/lessons/72411)

## 풀이

### 알고리즘

백트래킹 (Backtracking) / 조합 생성

### 접근 방법

각 주문에서 가능한 모든 조합을 DFS로 생성하고, 각 조합의 주문 횟수를 카운팅

각 코스 길이별로 가장 많이 주문된 조합을 찾아서 반환

### 풀이 과정:

1. **주문 정렬**

   - 각 주문 문자열을 알파벳 오름차순으로 정렬 (사전 순 정렬을 위해)

2. **조합 생성 (DFS)**

   - 각 주문에서 요청된 코스 길이만큼의 모든 조합을 생성
   - `dfs(depth, len, order, str, start)`:
     - `depth`: 현재 선택한 메뉴 개수
     - `len`: 목표 조합 길이
     - `order`: 정렬된 주문 문자열
     - `str`: 현재까지 만든 조합
     - `start`: 다음에 선택할 수 있는 시작 인덱스 (중복 방지)

3. **조합 카운팅**

   - HashMap에 조합과 주문 횟수를 저장
   - `count` 배열에 각 길이별 최대 주문 횟수 저장

4. **최대 주문 횟수 조합 선택**

   - 각 조합의 길이별로 최대 주문 횟수와 일치하는 조합만 선택
   - 최소 2명 이상의 손님으로부터 주문된 조합만 포함 (`count > 1`)

5. **정렬 및 반환**
   - 선택된 조합들을 사전 순으로 정렬하여 반환

### 시간 복잡도

O(2^n × m × k) - 각 주문에서 최대 2^n개의 조합이 가능하고, m개의 주문과 k개의 코스 길이를 처리 (n은 주문 길이, m은 주문 개수, k는 코스 개수)

### 코드

```java
import java.util.*;

class Solution {
    Map<String, Integer> mp = new HashMap<>();
    int count[] = new int[11];

    public void dfs(int depth, int len, String order, String str, int start) {
        if (depth == len) {
            int value = mp.getOrDefault(str, 0) + 1;
            mp.put(str, value);
            if (value > count[str.length()]) {
                count[str.length()] = value;
            }
            return;
        }

        for (int i = start; i < order.length(); i++) {
            dfs(depth + 1, len, order, str + order.charAt(i), i + 1);
        }
    }

    public String[] solution(String[] orders, int[] course) {
        List<String> answer = new ArrayList<>();

        // 각 코스 길이에 대해 조합 생성
        for (int c : course) {
            for (String o : orders) {
                // 주문 문자열을 알파벳 오름차순으로 정렬
                char ch[] = o.toCharArray();
                Arrays.sort(ch);
                String order = new String(ch);
                dfs(0, c, order, "", 0);
            }
        }

        // 각 길이별 최대 주문 횟수와 일치하는 조합만 선택
        for (String key : mp.keySet()) {
            if (count[key.length()] > 1 && count[key.length()] == mp.get(key)) {
                answer.add(key);
            }
        }

        // 사전 순으로 정렬하여 반환
        return answer.stream()
            .sorted()
            .toArray(String[]::new);
    }
}
```
