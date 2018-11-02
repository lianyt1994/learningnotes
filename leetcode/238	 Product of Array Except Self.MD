求数组中不包括自身其他数相乘的值，不能用除法，先从左边乘过去，再从右边乘过来，巧妙！
```JAVA
public class Solution {
  public int[] productExceptSelf(int[] nums) {
      int n = nums.length;
      int[] res = new int[n];
      res[0] = 1;
      for (int i = 1; i < n; i++) {
          res[i] = res[i - 1] * nums[i - 1];
      }
      int right = 1;
      for (int i = n - 1; i >= 0; i--) {
          res[i] *= right;
          right *= nums[i];
      }
      return res;
  }
}
```
