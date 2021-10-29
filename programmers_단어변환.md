### 프로그래머스 완전탐색 깊이/너비 우선 탐색(DFS/BFS)

#### 단어변환

* 코드 

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

class Solution {

    public static int answer = 100;
    public static Map<String, Integer> vMap;

    public int solution(String begin, String target, String[] words) {

        Map<String, ArrayList<String>> map = new HashMap<String, ArrayList<String>>();
        vMap = new HashMap<String, Integer>();
        String base = "";

        for(int i = 0 ; i <= words.length; i++) {
            if(base.equals("")) base = begin; 
            else base = words[i-1];

            ArrayList<String> list = new ArrayList<String>();
            for (int j = 0; j < words.length; j++) {

                int sameCnt = 0;

                for (int k = 0; k < words[j].length(); k++) {
                    if (base.charAt(k) == words[j].charAt(k))
                        sameCnt++;  
                }

                if (sameCnt == words[j].length() - 1) {
                    list.add(words[j]);
                }
            }
            map.put(base, list);
        }

        dfs(map, 0, begin, target);
        return (answer == 100 ? 0 : answer);
    }

    public static void dfs(Map<String, ArrayList<String>> map, int num, String begin, String target) {

        if(vMap.containsKey(begin)){ return;} 
        vMap.put(begin, 1);

        if(map.get(begin)!= null){
             ArrayList<String> list = map.get(begin);

            for(int i = 0 ; i < list.size(); i++) {
                if(target.equals(list.get(i))) {
                    answer = Math.min(num+1, answer); return;
                }
                dfs(map, num+1, list.get(i), target);
            }
        }

    }
}
```

학교다닐 때 배웠던 인접리스트처럼 구현해 보았다. 

단어는 한 글자만 고칠 수 있기 때문에, 일일히 비교하는 로직을 짜주었다.

처음에 한가지 케이스가 통과되지 않았다. 연결이 되는 관계인데, 빠지는 케이스들이 있었다.

이 문제는 그래프(?)의 방향성이 있는게 아니기 때문에, 다시 이어지는 모든 단어들은 자신의 인접리스트에 모두 포함시켜 주도록 수정했고, 대신 방문을 체크하기 위한 Map 변수를 하나 더 두었다. 