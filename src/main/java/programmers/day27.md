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