```java
public class Solution {
    public int nthUglyNumber(int n) {
        int[] ugly = new int[n];
        ugly[0] = 1;
        //分别记录2,3,5乘到了哪个位置
        int index2 = 0, index3 = 0, index5 = 0;
        //记录分别乘以2,3,5后的3个数
        int factor2 = 2, factor3 = 3, factor5 = 5;
        for(int i=1;i<n;i++){
            //选出这3个数中最小的
            int min = Math.min(Math.min(factor2,factor3),factor5);
            ugly[i] = min;
            //把选到的数指针往前走一步，然后乘以对应数值
            //注意：如果多个等于min（就是不同factor相等），都往前走一步，所以3个factor都要判断
            if(factor2 == min)
                factor2 = 2*ugly[++index2];
            if(factor3 == min)
                factor3 = 3*ugly[++index3];
            if(factor5 == min)
                factor5 = 5*ugly[++index5];
        }
        return ugly[n-1];
    }
}
```
