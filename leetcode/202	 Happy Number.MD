```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> set = new HashSet<>();
        while(set.add(n)){
            if(n==1 ){
                return true;
            }
            int result = 0;
            while(n>0){
                result += Math.pow(n%10,2);
                n = n/10;
            }
            n = result;
        }
        return false;
    }
}
```
