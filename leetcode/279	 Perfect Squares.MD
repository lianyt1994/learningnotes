Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

Example 1:

Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
Example 2:

Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.

<br>动态规划dp<br>
建立一个dp数组。在i从1到n的过程中，我们计算 dp[i - j * j] + 1最小的值。也就是减去一个平方数后我们比较这个剩余值的最小值，再加上1，就是我们的dp[i]
```java
public int numSquares(int n) {
    int[] dp = new int[n + 1];
    Arrays.fill(dp, Integer.MAX_VALUE);
    dp[0] = 0;
    //从1到n遍历找出每个点最小的可能性
    for(int i = 1; i <= n; ++i) {
        int min = Integer.MAX_VALUE;
        int j = 1;
        //从1开始，不断扩大和i的距离，获得到i的最小可能性
        while(i - j*j >= 0) {
            min = Math.min(min, dp[i - j*j] + 1);
            ++j;
        }
        dp[i] = min;
    }		
    return dp[n];
}
```
