第一个和最后一个不能同时拥有，就分两种情况，选其中最大的
```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 0){return 0;}
        if(nums.length == 1){return nums[0];}
        int n = nums.length;
        return Math.max(help(nums,0,n-2),help(nums,1,n-1));
        
        
    }
    
    public int help(int[] nums, int start,int end){
        int a=0;
        int b =0;
        for(;start<=end;start++){
            int temp =b;
            b=a+nums[start];
            a=Math.max(a,temp);
        }
        //这里要注意是取其中较大者不是最后一个！！！
        return Math.max(a,b);
    }
}
```
