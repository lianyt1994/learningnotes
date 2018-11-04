用O(1)返回i到j之间的和，用一个数组在构造的时候，存入0到i的和，需要的时候直接j-i就可以了
```java
class NumArray {

   int[] nums;

    public NumArray(int[] nums) {
        for(int i = 1; i < nums.length; i++)
            nums[i] += nums[i - 1];

        this.nums = nums;
    }

    public int sumRange(int i, int j) {
        if(i == 0)
            return nums[j];

        return nums[j] - nums[i - 1];
    }
}
```
