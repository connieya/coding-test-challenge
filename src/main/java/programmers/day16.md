# [[PCCE 기출문제] 10번 / 공원](https://school.programmers.co.kr/learn/courses/30/lessons/340198)

## solution

```java
import java.util.stream.IntStream;
import java.util.*;

class Solution {
    public int solution(int[] mats, String[][] park) {
        int n = park.length;
        int m = park[0].length;

        int [][]arr = new int[n][m];

        for(int i=0; i<n; i++){
            Arrays.fill(arr[i] , 1);
        }

        int answer = IntStream.of(mats).anyMatch(num -> num == 1)  ? 1 : -1;

        for(int i=1; i<n; i++) {
            for(int j=1; j<m; j++) {
                if(park[i][j].equals("-1")){
                    if(park[i-1][j-1].equals("-1") && park[i-1][j].equals("-1") && park[i][j-1].equals("-1")) {
                        arr[i][j] = Math.min(arr[i-1][j-1], Math.min(arr[i][j-1] , arr[i-1][j])) + 1;
                        int t = arr[i][j];
                        if(arr[i][j] > answer && IntStream.of(mats).anyMatch(num -> num == t)) {
                            answer = arr[i][j];
                        }
                    }
                }
            }
        }



        return answer;
    }
}
```

### 코드 설명

**1. 초기화 부분 (11-20줄)**

```java
int n = park.length;
int m = park[0].length();
int [][]arr = new int[n][m];
```

- `n`, `m`: 공원의 행과 열 크기
- `arr`: 각 위치에서 만들 수 있는 가장 큰 정사각형의 한 변 길이를 저장하는 DP 배열

```java
for(int i=0; i<n; i++){
    Arrays.fill(arr[i] , 1);
}
```

- 모든 위치를 1로 초기화 (각 위치는 최소 1x1 정사각형을 만들 수 있음)

```java
int answer = IntStream.of(mats).anyMatch(num -> num == 1)  ? 1 : -1;
```

- `mats` 배열에 1이 있으면 answer를 1로, 없으면 -1로 초기화
- 1x1 크기 돗자리를 가지고 있는지 확인

**2. 동적 프로그래밍 부분 (22-34줄)**

```java
for(int i=1; i<n; i++) {
    for(int j=1; j<m; j++) {
```

- (1,1)부터 시작하여 각 위치를 순회 (왼쪽 위, 위, 왼쪽을 참조해야 하므로)

```java
if(park[i][j].equals("-1")){
```

- 현재 위치가 빈 공간("-1")인지 확인

```java
if(park[i-1][j-1].equals("-1") && park[i-1][j].equals("-1") && park[i][j-1].equals("-1")) {
```

- 왼쪽 위, 위, 왼쪽 세 위치가 모두 빈 공간인지 확인
- 모두 빈 공간이어야 현재 위치를 포함한 더 큰 정사각형을 만들 수 있음

```java
arr[i][j] = Math.min(arr[i-1][j-1], Math.min(arr[i][j-1] , arr[i-1][j])) + 1;
```

- **핵심 로직**: 왼쪽 위, 위, 왼쪽 세 위치의 최소값 + 1
- 세 위치 중 가장 작은 정사각형 크기를 기준으로, 현재 위치를 포함하면 그보다 1 큰 정사각형을 만들 수 있음
- 예: 세 위치가 모두 2x2 정사각형을 만들 수 있다면, 현재 위치를 포함하면 3x3 정사각형 가능

```java
int t = arr[i][j];
if(arr[i][j] > answer && IntStream.of(mats).anyMatch(num -> num == t)) {
    answer = arr[i][j];
}
```

- 계산된 정사각형 크기(`t`)가 현재 답보다 크고, `mats` 배열에 해당 크기가 있는지 확인
- 조건을 만족하면 `answer` 업데이트

**3. 반환 (38줄)**

```java
return answer;
```

- 지민이가 깔 수 있는 가장 큰 돗자리 크기 반환 (없으면 -1)

### 알고리즘 요약

- **동적 프로그래밍**을 사용하여 각 위치에서 만들 수 있는 가장 큰 정사각형의 크기를 계산
- 왼쪽 위, 위, 왼쪽 세 위치의 최소값 + 1로 현재 위치의 정사각형 크기 결정
- 계산된 크기가 지민이가 가진 돗자리 크기(`mats`) 중에 있는지 확인하여 최대값 갱신

### 풀이

**알고리즘**

- 동적 프로그래밍 (Dynamic Programming)

**접근 방법**

- 각 위치에서 만들 수 있는 가장 큰 정사각형의 한 변 길이를 DP 배열에 저장
- 왼쪽 위, 위, 왼쪽 세 위치의 최소값 + 1로 현재 위치의 정사각형 크기 계산
- 계산된 크기가 지민이가 가진 돗자리 크기(`mats`) 중에 있는지 확인하여 최대값 갱신

**풀이 과정:**

1. DP 배열 초기화: 모든 위치를 1로 초기화 (최소 1x1 정사각형 가능)
2. 초기 답 설정: `mats` 배열에 1이 있으면 1, 없으면 -1로 초기화
3. DP 계산 (1,1)부터 시작:
   - 현재 위치가 빈 공간("-1")인지 확인
   - 왼쪽 위, 위, 왼쪽 세 위치가 모두 빈 공간인지 확인
   - 세 위치의 최소값 + 1로 현재 위치의 정사각형 크기 계산
   - 계산된 크기가 `mats` 배열에 있고 현재 답보다 크면 답 갱신
4. 최종 답 반환

**시간 복잡도**

- O(n × m) - 공원의 모든 칸을 한 번씩 순회 (n = 행, m = 열)
