```java
class Solution {
     public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        TreeSet<Integer> ts = new TreeSet<>();
        for (int i = 0; i < nums.length; i++) {
            if (i > k) ts.remove(nums[i-k-1]);
            Integer ceiling = ts.ceiling(nums[i]);
            Integer floor = ts.floor(nums[i]);
            if ((ceiling != null && (long)ceiling - (long)nums[i] <= t) || 
                (floor != null && (long)nums[i] - (long)floor <= t)) {
                return true;
            }
            
            ts.add(nums[i]);
        }
        
        return false;
    }
}
```
