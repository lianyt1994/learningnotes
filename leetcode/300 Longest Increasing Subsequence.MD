
动态规划
```java
 public int lengthOfLIS(int[] nums) {
    int len = nums.length;
    if (len == 0) {
        return 0;
    }
    // 状态的定义是：以 i 结尾的最长上升子序列的长度
    // 状态转移方程：之前比最后那个数字小的最长上升子序列的长度 + 1
    int[] dp = new int[len];
    Arrays.fill(dp, 1); // 如果只有 1 个元素，那么这个元素自己就构成了最长上升子序列，所以设置为 1 是合理的
    for (int i = 1; i < len; i++) { // 从第 2 个元素开始，逐个写出 dp 数组的元素的值
        int curVal = nums[i];
        for (int j = 0; j < i; j++) { // 找出比当前元素小的哪些元素的最小值
            if (curVal > nums[j]) {
                dp[i] = Integer.max(dp[j] + 1, dp[i]);
            }
        }
    }
    // 最后要全部走一遍，看最大值
    int res = dp[0];
    for (int i = 0; i < len; i++) {
        res = Integer.max(res, dp[i]);
    }
    return res;
}
```
![Image text](https://liweiwei1419.github.io/images/leetcode-solution/300-1.jpg)
<br>
```java
public int lengthOfLIS(int[] nums) {
    int[] tails = new int[nums.length];
    int size = 0;
    for (int x : nums) {
        int i = 0, j = size;
        while (i != j) {
            int m = (i + j) / 2;
            if (tails[m] < x)
                i = m + 1;
            else
                j = m;
        }
        tails[i] = x;
        if (i == size) ++size;
    }
    return size;
}
```
