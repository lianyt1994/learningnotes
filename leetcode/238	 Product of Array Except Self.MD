求数组中不包括自身其他数相乘的值，不能用除法，先从左边乘过去，再从右边乘过来，巧妙！
```JAVA
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] result = new int[nums.length];
        //先设好result[0]的值，因为下面没有为它赋初值
        result[0]=1;
        //用一个临时值来存从左边乘过来的数，和右边乘过来的数
        int temp=1;
        for(int i = 1;i<nums.length;i++){
            temp = temp*nums[i-1];
            result[i] = temp;
        }
        temp=1;
         for(int i = nums.length-2;i>=0;i--){
            temp = temp*nums[i+1];
            result[i] *= temp;
        }
        return result;
        
    }
}
```
