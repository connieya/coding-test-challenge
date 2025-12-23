# [조이스틱](https://school.programmers.co.kr/learn/courses/30/lessons/42860)

## 풀이

### 알고리즘

그리디 (Greedy)

### 접근 방법

조이스틱 조작 횟수는 **알파벳 변경 횟수**와 **커서 이동 횟수**의 합입니다.

각 문자를 변경하는 최소 조작 횟수를 계산하고, 연속된 'A'를 건너뛰는 최적 경로를 찾아 커서 이동 횟수를 최소화합니다.

### 풀이 과정:

1. **알파벳 변경 횟수 계산**

   - 각 문자에 대해 'A'에서 위로 가는 것과 아래로 가는 것 중 최소값 선택
   - 위로: `n - 'A'` (예: A→J는 9번)
   - 아래로: `'Z' - n + 1` (예: A→Z는 1번, A→Y는 2번)
   - `Math.min(n - 'A', 'Z' - n + 1)`로 최소값 계산

2. **커서 이동 최소 경로 찾기**

   - 기본값: `length - 1` (오른쪽으로만 가는 경우)
   - 각 위치 `i`에서 연속된 'A'를 건너뛰는 경우를 고려
   - `next`: `i+1` 위치부터 연속된 'A'의 끝 위치
   - **경로 1**: 오른쪽으로 `i`만큼 가고, 왼쪽으로 돌아가서 `length - next`만큼 가기
     - 이동 횟수: `i + (length - next) + min(i, length - next)`
   - **경로 2**: 왼쪽으로 먼저 가고, 오른쪽으로 돌아가기
   - 두 경로 중 최소값 선택

3. **결과 반환**
   - 알파벳 변경 횟수 + 커서 이동 최소 횟수

### 시간 복잡도

O(n²) - 각 위치에서 연속된 'A'를 찾는 while 루프가 최악의 경우 O(n)이므로 전체 O(n²)

### 코드

```java
import java.util.*;

class Solution {
    public int solution(String name) {
        int answer = 0;

        // 1. 알파벳 변경에 필요한 조작 횟수 계산
        for (char n : name.toCharArray()) {
            answer += Math.min(n - 'A', ('Z' - n + 1));
        }

        // 2. 커서 이동 최소 경로 찾기
        int length = name.length();
        int min = length - 1; // 기본값: 오른쪽으로만 가는 경우

        for (int i = 0; i < length; i++) {
            int next = i + 1;
            // 연속된 'A' 찾기
            while (next < length && name.charAt(next) == 'A') {
                next++;
            }
            // i 위치에서 오른쪽으로 가다가 왼쪽으로 돌아가는 경우와
            // 왼쪽으로 먼저 가다가 오른쪽으로 돌아가는 경우 중 최소값
            min = Math.min(min, i + length - next + Math.min(i, length - next));
        }

        return answer + min;
    }
}
```
