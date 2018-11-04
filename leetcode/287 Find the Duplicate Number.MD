找出数组中唯一重复的数，数组中的数是从1-n，没有0，所以nums[0]一定是起点，就相当于找到环的起点
```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0;
        int fast = 0;
        
        while(true){
            slow = nums[slow];
            fast =nums[nums[fast]];
            if(fast == slow)break;
        }
        fast = 0;
        while(true){
            slow = nums[slow];
            fast = nums[fast];
            if(fast == slow)break;
        }
        return slow;
            
    }
}
```
