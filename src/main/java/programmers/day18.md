# [혼자 놀기의 달인](https://school.programmers.co.kr/learn/courses/30/lessons/131130)

## 풀이

### 알고리즘

Union-Find (Disjoint Set Union)

### 접근 방법

상자 번호를 따라가면서 사이클을 형성하는 그룹을 찾는 문제

Union-Find 자료구조를 사용하여 연결된 상자들을 하나의 그룹으로 묶기

각 그룹의 크기를 계산하고, 가장 큰 두 그룹의 크기를 곱하여 최고 점수 구하기

### 풀이 과정:

1. **Union-Find 초기화**

   - 각 상자 번호를 자신의 부모로 초기화 (1부터 시작)

2. **상자 연결 (Union)**

   - 상자 i+1에 cards[i]가 들어있으므로, 상자 i+1과 상자 cards[i]를 연결
   - Union 연산으로 두 상자를 같은 그룹으로 묶기

3. **그룹 크기 계산**

   - 각 상자의 루트를 찾아서 그룹별로 크기 카운팅
   - HashMap을 사용하여 각 그룹의 크기 저장

4. **최고 점수 계산**
   - 그룹 크기를 정렬
   - 그룹이 1개 이하면 0 반환
   - 가장 큰 두 그룹의 크기를 곱하여 반환

### 시간 복잡도

O(n × α(n)) - Union-Find 연산의 시간 복잡도 (n은 cards의 길이, α는 역 아커만 함수로 거의 상수)

### 코드

```java
import java.util.*;

class Solution {
    int[] parent;

    public int solution(int[] cards) {
        int n = cards.length;
        parent = new int[n + 1];

        // Union-Find 초기화
        for (int i = 1; i <= n; i++) {
            parent[i] = i;
        }

        // 상자 연결
        for (int i = 0; i < n; i++) {
            int a = findParent(i + 1);
            int b = findParent(cards[i]);
            if (a != b) {
                union(i + 1, cards[i]);
            }
        }

        // 그룹 크기 계산
        Map<Integer, Integer> groupSize = new HashMap<>();
        for (int i = 1; i <= n; i++) {
            int root = findParent(i);
            groupSize.put(root, groupSize.getOrDefault(root, 0) + 1);
        }

        // 그룹 크기 정렬
        List<Integer> sizes = new ArrayList<>(groupSize.values());
        Collections.sort(sizes);

        // 그룹이 1개 이하면 0 반환
        if (sizes.size() <= 1) {
            return 0;
        }

        // 가장 큰 두 그룹의 크기 곱하기
        return sizes.get(sizes.size() - 1) * sizes.get(sizes.size() - 2);
    }

    // Find 연산 (경로 압축)
    private int findParent(int x) {
        if (x != parent[x]) {
            parent[x] = findParent(parent[x]);
        }
        return parent[x];
    }

    // Union 연산
    private void union(int a, int b) {
        a = findParent(a);
        b = findParent(b);
        if (a < b) {
            parent[b] = a;
        } else {
            parent[a] = b;
        }
    }
}
```
