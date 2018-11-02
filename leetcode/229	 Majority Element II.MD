超过1/3的数，两个最大的数之间不用互相减，只有其他的能减他们，这样count一定可以大于0
```java
public List<Integer> majorityElement(int[] nums) {
    if (nums == null || nums.length == 0)
      return new ArrayList<Integer>();
    List<Integer> result = new ArrayList<Integer>();
    int number1 = nums[0], number2 = nums[0], count1 = 0, count2 = 0, len = nums.length;
    for (int i = 0; i < len; i++) {
      if (nums[i] == number1)
        count1++;
      else if (nums[i] == number2)
        count2++;
      else if (count1 == 0) {
        number1 = nums[i];
        count1 = 1;
      } else if (count2 == 0) {
        number2 = nums[i];
        count2 = 1;
      } else {
        count1--;
        count2--;
      }
    }
    //最后还要判断一下是不是真的超过1/3，因为有可能3,3,3,3,3,3,3,3，3,3,3,3,1
    count1 = 0;
    count2 = 0;
    for (int i = 0; i < len; i++) {
      if (nums[i] == number1)
        count1++;
      else if (nums[i] == number2)
        count2++;
    }
    if (count1 > len / 3)
      result.add(number1);
    if (count2 > len / 3)
      result.add(number2);
    return result;
}
```
