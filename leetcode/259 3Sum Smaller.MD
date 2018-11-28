```java
public class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        Arrays.sort(nums);
        int count = 0;
        for(int i=0; i<nums.length-2; i++) {
            int j=i+1, k=nums.length-1;
            while (j<k) {
                if (nums[i]+nums[j]+nums[k] < target) {
                    //注意这边不是加一，因为第三个数从k-j之间的都可以
                    count += k-j;
                    j ++;
                } else {
                    k --;
                }
            }
        }
        return count;
    }
}
```
