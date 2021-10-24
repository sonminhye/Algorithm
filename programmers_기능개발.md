### 프로그래머스 스택/큐

#### 기능개발

* 코드 

```java
import java.util.LinkedList;
import java.util.Queue;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        int[] answer = {};

        Queue<Integer> queue = new LinkedList<Integer>();
        Queue<Integer> remainDays = new LinkedList<Integer>();

        for(int i = 0; i< progresses.length; i++) {
            int remainPercent = 100 - progresses[i];
            queue.add(remainPercent / speeds[i] + (remainPercent % speeds[i] > 0 ? 1 : 0));
        }

        int peekNum = queue.poll();
        int depNum = 1;

        while(!queue.isEmpty()) {
            if(peekNum < queue.peek()) {
                remainDays.add(depNum);
                depNum = 1;
                peekNum = queue.peek();             
            }else {
                depNum++;
            }
            queue.poll();
        }

        remainDays.add(depNum);

        answer = new int[remainDays.size()];

        for(int i = 0 ; i < answer.length;i++) {
            answer[i] = remainDays.poll();
        }

        return answer;
    }
}
```

스택/큐 문제라서 큐를 활용해서 풀었는데, 큐를 꼭 사용할 필요는 없는 것 같다.

자바 큐를 써본지가 오래되서 써볼 겸 풀어봤다.

다른사람들의 풀이를 봤는데, 아주 간결하게 푼 코드들도 많아서 놀랐다. 

더욱 효율적인 방법이 없을지 항상 생각해보고 제출해야겠다. ^^;;