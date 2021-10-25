### 프로그래머스 완전탐색

#### 모의고사

* 코드 

```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] answers) {
        int[] answer = new int[3];
        int[] num = new int[3];

        int[] person1 = { 1, 2, 3, 4, 5 };
        int[] person2 = { 2, 1, 2, 3, 2, 4, 2, 5 };
        int[] person3 = { 3, 3, 1, 1, 2, 2, 4, 4, 5, 5 };
        int max = 0;

        for (int i = 0; i < answers.length; i++) {
            if (person1[i % 5] == answers[i]) {
              num[0]++; max = max < num[0] ? num[0] : max; 
            }
            if (person2[i % 8] == answers[i]) {
              num[1]++; max = max < num[1] ? num[1] : max;
            }
            if (person3[i % 10] == answers[i]) {
              num[2]++; max = max < num[2] ? num[2] : max;
            }
        }

        for(int i = 0 ; i < num.length; i++) {
            if(num[i] == max) answer[i] = i+1;
        }

        return Arrays.stream(answer).filter(i -> i!=0).toArray();
    }
}
```

반복문을 돌면서 최대값을 구하고, 해당 값으로 다시 비교하였다. 

Stream filter를 사용해 int[] 를 반환하였다.