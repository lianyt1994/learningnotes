//用set要提前把多出来的排除掉
```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Set<Integer> set = new HashSet<>();
        for(int i=0;i<nums.length;i++){ 
            if(set.size()>k)set.remove(nums[i-k-1]);
            if(!set.add(nums[i]))return true;
           
        }
        return false;
    }
}
```
//用map可以value存它最后的位置（因为后面出现的会把之前的覆盖了），再判断位置是否合法
```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(nums[i])) {
            if (i - map.get(nums[i]) <= k) return true;
        }
        map.put(nums[i], i);
    }
    return false;
}
```
