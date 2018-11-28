```java
public class Solution {
    public boolean canPermutePalindrome(String s) {
        char[] sa = s.toCharArray();
        int[] f = new int[256];
        for(int i=0; i<sa.length; i++) f[sa[i]] ++;
        boolean single = false;
        for(int i=0; i<f.length; i++) {
            if (f[i] % 2 == 1) {
                if (!single) single = true; else return false;
            }
        }
        return true;
    }
}
```
```java
public class Solution {
    public boolean canPermutePalindrome(String s) {
        int[] f = new int[256];
        char[] sa = s.toCharArray();
        for(int i=0; i<sa.length; i++) f[sa[i]] ++;
        int even = 0, odd = 0;
        for(int i=0; i<f.length; i++) {
            if ((f[i] & 1) == 0) even ++; else odd ++;
        }
        if ((sa.length & 1) == 0) {
            return odd == 0;
        } else {
            return odd == 1;
        }
    }
}
```
