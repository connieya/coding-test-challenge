# [프로그래머스 - 키패드 누르기 ](https://school.programmers.co.kr/learn/courses/30/lessons/67256?language=java)

## solution 

```java
class Solution {
    public String solution(int[] numbers, String hand) {
        int NumberPad[][] = {
            {3, 1}, //0
            {0, 0}, // 1
            {0, 1}, // 2
            {0, 2}, //3
            {1, 0}, //4
            {1, 1}, //5
            {1, 2}, //6
            {2, 0}, //7
            {2, 1}, //8
            {2, 2} //9
        };
        int left[] = {3, 0};
        int right[] = {3, 2};
        int L_dis, R_dis;
        StringBuilder sb = new StringBuilder();
        for (int number : numbers) {
            if (number == 1 || number == 4 || number == 7) {
                sb.append("L");
                left[0] = NumberPad[number][0];
                left[1] = NumberPad[number][1];
            } else if (number == 3 || number == 6 || number == 9) {
                sb.append("R");
                right[0] = NumberPad[number][0];
                right[1] = NumberPad[number][1];
            } else {
                L_dis = Math.abs(left[0] - NumberPad[number][0]) + Math.abs(left[1] - NumberPad[number][1]);
                R_dis = Math.abs(right[0] - NumberPad[number][0]) + Math.abs(right[1] - NumberPad[number][1]);
                if (L_dis > R_dis) {
                    sb.append("R");
                    right[0] = NumberPad[number][0];
                    right[1] = NumberPad[number][1];
                } else if (L_dis < R_dis) {
                    sb.append("L");
                    left[0] = NumberPad[number][0];
                    left[1] = NumberPad[number][1];
                } else {
                    if (hand.equals("right")) {
                        sb.append("R");
                        right[0] = NumberPad[number][0];
                        right[1] = NumberPad[number][1];
                    } else {
                        sb.append("L");
                        left[0] = NumberPad[number][0];
                        left[1] = NumberPad[number][1];
                    }
                }
            }
        }
        return sb.toString();
    }
}
```

### 풀이

**알고리즘**

- 시뮬레이션 + 맨해튼 거리 (Manhattan Distance)

**접근 방법**

- 키패드를 2차원 좌표로 표현하여 각 숫자의 위치를 저장
- 왼손과 오른손의 현재 위치를 추적
- 가운데 열(2, 5, 8, 0)의 경우 맨해튼 거리를 계산하여 더 가까운 손 선택
- 거리가 같으면 손잡이(hand)에 따라 결정

**풀이 과정:**

1. **키패드 좌표 초기화**: 각 숫자(0~9)의 2차원 좌표를 배열로 저장
    - 예: 0은 (3, 1), 1은 (0, 0), 2는 (0, 1) 등
2. **손 위치 초기화**:
    - 왼손: (3, 0) - * 키패드
    - 오른손: (3, 2) - # 키패드
3. **각 숫자에 대해**:
    - **왼쪽 열 (1, 4, 7)**: 왼손 사용, 위치 업데이트
    - **오른쪽 열 (3, 6, 9)**: 오른손 사용, 위치 업데이트
    - **가운데 열 (2, 5, 8, 0)**:
        - 왼손과 오른손의 맨해튼 거리 계산
        - 거리가 더 가까운 손 사용
        - 거리가 같으면 `hand` 값에 따라 결정 (오른손잡이면 오른손, 왼손잡이면 왼손)
        - 사용한 손의 위치 업데이트
4. 결과 문자열 반환

**시간 복잡도**

- O(n) - numbers 배열의 길이만큼 순회 (n = numbers.length)