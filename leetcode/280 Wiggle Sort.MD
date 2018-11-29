遍历一遍数组, 如果是奇数位置并且其值比下一个大,则交换其值, 如果是偶数位置并且其值比下一个小, 则交换其值. 时间复杂度是O(N)
```JAVA
public class Solution {
    public void wiggleSort(int[] nums) {
        for(int i=0;i<nums.length;i++)
            if(i%2==1){
               if(nums[i-1]>nums[i]) swap(nums, i);
            }else if(i!=0 && nums[i-1]<nums[i]) swap(nums, i);
    }
    public void swap(int[] nums, int i){
          int tmp=nums[i];
          nums[i]=nums[i-1];
          nums[i-1]=tmp;
    }
}

```
