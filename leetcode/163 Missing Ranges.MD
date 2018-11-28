```JAVA
public class Solution {
    private String range(int lower, int upper) {
        if (lower == upper) return Integer.toString(lower);
        return lower + "->" + upper;
    }
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> ranges = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            ranges.add(range(lower, upper));
            return ranges;
        }
        if (lower < nums[0]) ranges.add(range(lower, nums[0]-1));
        for(int i=0; i<nums.length-1; i++) {
            if (nums[i] + 1 < nums[i+1]) ranges.add(range(nums[i]+1, nums[i+1]-1));
        }
        if (nums[nums.length-1] < upper) ranges.add(range(nums[nums.length-1]+1, upper));
        return ranges;
    }
}

```
