### 프로그래머스 동적계획법(Dynamic Programming)

#### 정수 삼각형

* 코드 

```java
import java.util.Arrays;

class Solution {
    public int solution(int[][] triangle) {
        int answer = 0;

        int dp[][] = new int[500][500];
        dp[0][0] = triangle[0][0];
        dp[1][0] = triangle[1][0] + dp[0][0];
        dp[1][1] = triangle[1][1] + dp[0][0];

        for (int i = 2; i < triangle.length; i++) {
            for (int j = 0; j < i + 1; j++) {
                if(i == j) {
                    dp[i][j] = triangle[i][j] + dp[i-1][j-1];
                }else if(j==0){                 
                    dp[i][j] = triangle[i][j] + dp[i-1][j];
                }else {
                    dp[i][j] = triangle[i][j] + Math.max(dp[i-1][j-1] , dp[i-1][j]);
                }
            }
        }

        int[] intArr = dp[triangle.length-1];
        answer = Arrays.stream(intArr).max().getAsInt();
        return answer;
    }
}
```

