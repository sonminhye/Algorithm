### 프로그래머스 정렬

#### K번째수

* 코드 

```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for(int i = 0 ; i < commands.length; i++) {
            int[] temp = new int[(commands[i][1] - commands[i][0]) + 1];
            for(int j = (commands[i][0]-1); j <= (commands[i][1]-1); j++) {
                temp[j-(commands[i][0]-1)] = array[j];
            }

            answer[i] = Arrays.stream(temp).sorted().toArray()[commands[i][2]-1];
        }

        return answer;
    }
}
```

정렬 알고리즘을 직접 구현해 보고 싶었는데, Stream 사용에 좀 더 익숙해져보고자 사용해보았다.