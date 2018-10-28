Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]).

Find the minimum element.

You may assume no duplicate exists in the array.

Example 1:

Input: [3,4,5,1,2] 
Output: 1
Example 2:

Input: [4,5,6,7,0,1,2]
Output: 0 
```java
public class Solution {
    public int findMin(int[] num) {
        if (num == null || num.length == 0) {
            return 0;
        }
        if (num.length == 1) {
            return num[0];
        }
        int start = 0, end = num.length - 1;
        //用左右的方法可以保证数组不会越界
        while (start < end) {
            int mid = (start + end) / 2;
            //先判断一下中间节点
            if (mid > 0 && num[mid] < num[mid - 1]) {
                return num[mid];
            }
            //走右边的可能性比较少就先走右边
            if (num[start] <= num[mid] && num[mid] > num[end]) {
                start = mid + 1;
                //其他的再走左边
            } else {
                end = mid - 1;
            }
        }
        return num[start];
    }
}
```
