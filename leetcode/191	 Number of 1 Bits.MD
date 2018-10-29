```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int result = 0;
        //用不等号是因为2147483648 (10000000000000000000000000000000)是负的
        while(n!=0){
            result += n &1;
            //用>>>是因为2147483648 (10000000000000000000000000000000)高位是1
            n = n>>>1;
        }
        return result;
        
    }
}
```
