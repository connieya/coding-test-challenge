# [프로그래머스 - 멀쩡한 사각형](https://school.programmers.co.kr/learn/courses/30/lessons/62048?language=java)

## solution

```java
class Solution {
    public long solution(long w, long h) {
        long answer = w*h;
        answer -= (w+h - gcd(w,h));
        return answer;
    }
    
    public long gcd(long a, long b)  {
        return (b==0) ? a: gcd(b , a%b);
    }
}
```
