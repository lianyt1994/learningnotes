```java
public class Solution {
    public boolean isStrobogrammatic(String num) {
        char[] na = num.toCharArray();
        int i=0, j=na.length-1;
        while (i<=j) {
            if ((na[i] == '0' && na[j] == '0')
            || (na[i] == '1' && na[j] == '1')
            || (na[i] == '8' && na[j] == '8')
            || (na[i] == '6' && na[j] == '9')
            || (na[i] == '9' && na[j] == '6')) {
                i ++;
                j --;
            } else {
                return false;
            }
        }
        return true;
    }
}

```
 
