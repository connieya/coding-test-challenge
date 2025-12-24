# [괄호 변환](https://school.programmers.co.kr/learn/courses/30/lessons/60058)

## 풀이

### 알고리즘

재귀 (Recursion) / 분할 정복 (Divide and Conquer)

### 접근 방법

균형잡힌 괄호 문자열을 재귀적으로 분리하여 올바른 괄호 문자열로 변환

문제에서 제시한 알고리즘을 그대로 구현:

1. 빈 문자열이면 빈 문자열 반환
2. 균형잡힌 괄호 문자열 u, v로 분리
3. u가 올바른 괄호 문자열이면 v를 재귀 처리 후 u에 이어붙이기
4. u가 올바른 괄호 문자열이 아니면 특정 규칙에 따라 변환

### 풀이 과정:

1. **균형잡힌 괄호 문자열 분리**

   - 문자열을 순회하며 '('와 ')'의 개수가 같아지는 지점을 찾아 u, v로 분리
   - `balance` 변수로 '('는 +1, ')'는 -1로 카운팅

2. **올바른 괄호 문자열 확인**

   - u의 첫 번째 문자가 '('이고 마지막 문자가 ')'이면 올바른 괄호 문자열
   - 이 경우 v를 재귀 처리한 결과를 u에 이어붙여 반환

3. **올바르지 않은 경우 변환**
   - `"(" + solution(v) + ")" + reverse(u)` 형태로 변환
   - `reverse(u)`: u의 첫 번째와 마지막 문자를 제거하고 나머지 괄호 방향 뒤집기

### 시간 복잡도

O(n²) - 각 재귀 호출마다 문자열을 순회하고, 최악의 경우 n번 재귀 호출

### 코드

```java
class Solution {
    public String solution(String p) {
        if (p.length() < 1) return "";

        int balance = 0;
        int pivot = 0;

        // 균형잡힌 괄호 문자열 u를 찾기
        do {
            balance += (p.charAt(pivot++) == '(') ? 1 : -1;
        } while (balance != 0);

        String u = p.substring(0, pivot);
        String v = solution(p.substring(pivot));

        // u가 올바른 괄호 문자열인지 확인
        if (u.charAt(0) == '(' && u.charAt(u.length() - 1) == ')') {
            return u + v;
        }

        // 올바르지 않은 경우 변환
        return "(" + v + ")" + reverse(u);
    }

    // u의 첫 번째와 마지막 문자를 제거하고 나머지 괄호 방향 뒤집기
    private String reverse(String str) {
        StringBuilder sb = new StringBuilder();
        String middle = str.substring(1, str.length() - 1);
        for (char c : middle.toCharArray()) {
            sb.append((c == '(') ? ')' : '(');
        }
        return sb.toString();
    }
}
```
