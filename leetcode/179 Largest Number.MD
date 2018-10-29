Given a list of non negative integers, arrange them such that they form the largest number.

Example 1:

Input: [10,2]
Output: "210"
Example 2:

Input: [3,30,34,5,9]
Output: "9534330"
Note: The result may be very large, so you need to return a string instead of an integer.

```java
public class Solution {
    public String largestNumber(int[] nums) {
        if(nums == null || nums.length == 0)
            return null;
        String[] str = new String[nums.length];
        for(int i = 0; i < nums.length; i ++) {
            str[i] = String.valueOf(nums[i]);
        }
        //自己写比较器
        Arrays.sort(str, new Comparator<String>() {
            public int compare(String a, String b) {
                String leftRight = a + b;
                String rightLeft = b + a;
                //记得加上负号
                return -leftRight.compareTo(rightLeft);
            }
        });
        StringBuilder sb = new StringBuilder();
        for(String s : str) {
            sb.append(s);
        }
        //删掉前面为0的数
        while(sb.charAt(0) == '0' && sb.length() > 1)
            sb.deleteCharAt(0);
        return sb.toString();
    }
}
```
