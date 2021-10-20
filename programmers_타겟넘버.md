### 프로그래머스 깊이/너비 우선 탐색(DFS/BFS)

#### 타겟넘버

* 코드

```java
class Solution {
	int target;
	int[] numbers;
	int answer = 0;

	public int solution(int[] numbers, int target) {
		answer = 0;
		this.numbers = numbers;
		this.target = target;
		dfs(0, 0, numbers);
		return answer;
	}

	public void dfs(int sum, int i, int[] numbers) {
		if (i == numbers.length) {
			if (sum == target) {
				answer++;
			}
			return;
		}
		dfs(sum + numbers[i], i + 1, numbers);
		dfs(sum - numbers[i], i + 1, numbers);
	}
}
```

오랜만의 알고리즘이라 조금 헤맸다.

쉽게 생각하면 됐는데, 되려 너무 어렵게 생각을 한 것 같은 문제다. 

나는 dfs 함수를 재귀로 호출하여 문제를 풀었는데, 조금 더 코드를 간결하게 바꿀 수 있을 것 같다.



```java
public int solution(int[] numbers, int target) {
	answer = 0;
	answer = dfs(0, 0, numbers, target);
	return answer;
}

public int dfs(int sum, int i, int[] numbers, target) {
	if (i == numbers.length) {
		if (sum == target) {
       return 1;
		}else return 0;
	}
	return dfs(sum + numbers[i], i + 1, numbers, target) + dfs(sum - numbers[i], i + 1, numbers, target);
}

```
위와 같이, dfs 함수를 int 를 반환하는 함수로 만들고, target 변수까지 함께 넘기는 방식으로도 풀 수 있을 것 같다. 

함수에 너무 많은 파라미터를 넣어서 호출해야 되는 게 좋은 방법인지는 모르겠지만, 위처럼 바꿔서 제출했을 때도 통과는 됐다.

오랜만에 푸는 문제라 헤맸는데, 여러 유형의 문제들을 풀며 감을 익혀야겠다.

