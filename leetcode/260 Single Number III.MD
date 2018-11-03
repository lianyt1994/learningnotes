这道题可以用HashMap来做，但是对于空间复杂度要求很高。题目要求的是常量的空间复杂度；

参考网上别人的思路，发现了一种非常巧妙的方法；

首先遍历整个数组，讲所有的值相异或，那么最后的值肯定是两个相异的值异或的结果。

这两个值不同，那么肯定有一位的二进制值不同，那么这个位相异或的结果肯定是这位的数值为1；

那么我们寻找这个数值位为1的位，

这里采用非常巧妙的方法：resTwo &= -resTwo; 因为int整数在java中是按照补码的方式来的，那么正数和它负值按位与的结果是原始最右边非0位的数字为1，其余位都为0；

这样我们把原来的数组分为两个部分，一部分是和resTwo按位与的结果为0的，另一部分的结果和resTwo按位与的结果为1的，并且那两个不相等的数分别落在这两个组中；

这样分别对两组的数异或，即可得到这两个数。


```java
public class Solution {
    public int[] singleNumber(int[] nums) {
        int resTwo = 0;
        int[] res = new int[2];;
        for(int i = 0; i < nums.length; i++){
            resTwo ^= nums[i];
        }
        // find the rigthest bit which is not 0
        //得到不为0的最小的一位
        resTwo &= -resTwo;
        for(int i = 0; i < nums.length; i++){
            //分成两批，一批有这个1的，一批没有这个1的
            if((nums[i] & resTwo) == 0){
                res[0] ^= nums[i];
            } else{
                res[1] ^= nums[i];
            }
        }
        return res;
    }
}
```
