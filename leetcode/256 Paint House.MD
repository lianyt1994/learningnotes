```java
public class Solution {
    public int minCost(int[][] costs) {
    if(costs.length==0) return 0;
    int prevR= costs[0][0];
    int prevG = costs[0][1];
    int prevB = costs[0][2];
    for(int i=1; i<costs.length; i++){
        int curR = Math.min(prevG,prevB)+costs[i][0];
        int curG = Math.min(prevR,prevB)+costs[i][1];
        int curB = Math.min(prevR,prevG)+costs[i][2];
        prevR = curR;
        prevG = curG;
        prevB = curB;
    }
    return Math.min(Math.min(prevR,prevG),prevB);

    }
}
```
```
class Solution {
    public:
        int minCost(vector<vector<int>>& costs) {
            if (costs.empty() || costs[0].empty()) return 0;
            vector<vector<int>> dp = costs;
            for (int i = 1; i < dp.size(); ++i) {
                for (int j = 0; j < 3; ++j) {
                    dp[i][j] += min(dp[i - 1][(j + 1) % 3], dp[i - 1][(j + 2) % 3]);
                }
            }
            return min(min(dp.back()[0], dp.back()[1]), dp.back()[2]);
        }
};
```
