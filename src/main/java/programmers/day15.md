# [붕대 감기](https://school.programmers.co.kr/learn/courses/30/lessons/250137)

## solution

```java
class Solution {
    public int solution(int[] bandage, int health, int[][] attacks) {
        int prevTime = 0;
        int maxHealth = health;
        int t = bandage[0];
        int x = bandage[1];
        int y = bandage[2];

        for (int[] attack : attacks) {
            int time = attack[0];
            int value = attack[1];

            // 체력 회복
            int tt = time - prevTime - 1;

            // 초당 회복
            health += tt * x;

            // 추가 회복
            if (tt >= t) {
                health += y * (tt / t);
            }
            health = Math.min(health, maxHealth);

            // 공격
            health -= value;

            if (health <= 0) return -1;

            // 시간이 지나감
            prevTime = time;
        }

        return health;
    }
}
```

### 풀이

**알고리즘**

- 시뮬레이션

**접근 방법**

- 공격 시간 순서대로 시뮬레이션하며 체력 회복과 공격 처리
- 이전 공격 시간과 현재 공격 시간 사이의 시간 차이를 계산하여 체력 회복
- 연속 회복 시간이 t초 이상이면 추가 회복량(y) 적용

**풀이 과정:**

1. 각 공격에 대해:
   - 이전 공격 시간과 현재 공격 시간 사이의 시간 차이(tt) 계산
   - 시간 차이만큼 초당 회복량(x) 적용
   - 연속 회복 시간이 t초 이상이면 추가 회복량(y) 적용 (tt/t번)
   - 최대 체력 제한 적용
   - 공격으로 체력 감소
   - 체력이 0 이하가 되면 -1 반환
2. 모든 공격 후 남은 체력 반환
